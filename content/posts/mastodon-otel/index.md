+++
title = 'Mastodon & OpenTelemetry'
date = 2024-11-11
tags = [
    'OpenTelemetry'
]
+++

I joined Datadog in January 2024, and in February, my colleague [Ara Pulido] connected me with [Mastodon] to help
onboard their backend to Datadog.

Mastodon had been using Datadog for a year through Datadog's Open Source Program, primarily to monitor their hosts,
Kubernetes cluster, logs, and database performance. However, they were exploring OpenTelemetry to get vendor agnostic
instrumentation into their backend.

I wrote about this on [Datadog's Open Source Hub], but I wanted to share some personal and technical insights that
didn't quite fit in that post—so here we go.

## Initial Challenges

When I started examining the [source code], I discovered that Mastodon is written in Ruby. Although I had previously
worked with Ruby, creating a sample Ruby app is quite different from working on a real-world application.
Fortunately, it worked out well.

The community had already begun developing something similar. In November 2022, [Robb Kidd] submitted a [pull request]
to add OpenTelemetry (OTel) to Mastodon, and I built a solution on top of that by [integrating the OTel Collector][julianos-pr].

## The PR with the Collector

Even though this wasn't the pull request that ultimately got merged, I'd like to take a moment to discuss a suggestion I made.

### The Collector

Since Mastodon wanted to enable users to send telemetry data to any observability backend, I aimed to allow developers to
configure their own Collector as needed, but creating a minimal custom Collector containing only the required components for
each use-case.

To achieve this, I used a multi-stage Dockerfile. First, it uses the OpenTelemetry Collector Builder (OCB) to create a
minimal Collector distribution based on a manifest file specifying which components should be included.
It then runs the Collector with its configuration file.

Here's an example of what a `manifest.yaml` file looks like:

{{% snippet manifest.yaml yaml %}}

Below is an example of the `Dockerfile`:

{{% snippet Dockerfile Dockerfile %}}

And finally, here's an example of the `otelcol-config.yaml` file:

{{< alert >}}
Note that you can only use the components previously added to the manifest file, as the custom Collector includes only
those components. If you try to use a component not defined in the manifest, the Collector will fail to start.
{{< /alert >}}

In the pull request, I also added a `TELEMETRY_BACKEND` build argument, which selects a different manifest file depending
on the observability backend the user wants to send data to. For example, the Datadog manifest includes the
Datadog-specific components, while the default manifest includes only the `OTLP` and vendor-agnostic components.

This setup was designed to allow users to contribute their own manifests with additional components as needed.

To learn more about the OCB, refer to the official OpenTelemetry documentation: [Building a custom collector].

### The Instrumentation

The main difference between Robb's initial PR and mine, on the instrumentation side, was that instead of using
`opentelemetry-instrumentation-all`, I suggested adding only the specific dependencies we needed.

This approach is more verbose and requires additional maintenance, but it gives us greater control over what we're
instrumenting. It also aligns with the goal of building a minimal Collector distribution.

Rather than importing everything automatically, we define exactly what we want, use only what we need, and keep the
setup streamlined.

## The Collector Configuration

After the Mastodon team's PR was merged, they began sending OpenTelemetry traces to Datadog via the Collector.

This sparked an invaluable back-and-forth exchange between [Renaud Chaput], [Tim Campbell], and me, for which I'll be
forever grateful.

As a representative of the community, users, and customers within Datadog, understanding their pain points and challenges
with sending OTel data to Datadog is one of the most important aspects of my role.

In the [Datadog Open Source Hub][Datadog's Open Source Hub] blog post, I discussed how [Inferred Services] significantly
improved Mastodon's usability. Here, I want to focus on specific Collector configurations that helped them navigate the
OTel ecosystem within Datadog more effectively.

### Resource Processor

In the snippet below, the [resourceprocessor] component is used to set an attribute:
`deployment.environment.name=development`.

When OTel data arrives in Datadog with this attribute, the service is tagged accordingly, making it easier for the team
to navigate and analyze their data in Datadog.

```yaml
processors:
  [...]
  resource:
    attributes:
      - key: deployment.environment.name
        value: "development"
        action: upsert
```

### Transform Processor

Working with the [transformprocessor] was a valuable learning experience for me. Although I was aware of the component,
I had never used it myself.

Mastodon wanted assistance in improving the naming of their spans beyond the default Ruby instrumentation name.

They would like the values from `code.namespace` and `code.function` combined. If you're unfamiliar with these terms,
as I initially was, here's an example:

A namespace might look like `Api::V1::Timelines::PublicController`, while the function could be `show`.

The snippet below demonstrates how these two values are concatenated with a `#` in between, resulting in
`Api::V1::Timelines::PublicController#show`.

```yaml
processors:
  [...]
  transform:
    error_mode: ignore
    trace_statements:
      - context: span
        conditions:
          - attributes["code.namespace"] != nil
        statements:
          - set(attributes["resource.name"], Concat([attributes["code.namespace"], attributes["code.function"]], "#"))
```

{{< alert >}}

Note that we are not actually changing the span name but rather setting the resource name.
This is a Datadog-specific concept that we won't explore here, but if you're interested, you can
learn more in the [Resources glossary](https://docs.datadoghq.com/tracing/glossary/#resources).
{{< /alert >}}

### Tail Sampling Processor

I vividly remember [Reese Lee's presentation] on [Tail-Based Sampling] at KubeCon EU 2022. It was my first
introduction to the concept, and I was truly impressed by its potential.
Reese delivered a fantastic talk with a great hands-on demo.

Another noteworthy talk was from [Vijay and Aishwarya from eBay] at this year's (2024) Observability Day EU.
They shared that they sample only 1% of their traces, which, due to their high traffic volume, is sufficient 🤯.

Tail sampling has a challenge when using multiple Collectors: you **must** ensure that all spans from a trace
reach the same Collector, or else you'll end up with broken traces.

In Mastodon's case, I was fortunate—they're using a single Collector instance, which made configuring it much easier.

Initially, I suggested sampling 25% of traces, plus all errors, but Tim found that 10%, plus errors, met their needs.

Below is the `tail_sampling` processor definition for this setup.

```yaml
processors:
  [...]
  tail_sampling:
    policies:
      [
        {
          name: errors-policy,
          type: status_code,
          status_code: {status_codes: [ERROR]}
        },
        {
          name: randomized-policy,
          type: probabilistic,
          probabilistic: {sampling_percentage: 10}
        },
      ]
```

Another important point about tail sampling is that if you're calculating metrics from spans using components like
[spanmetricsconnector] or [datadogconnector], you need to ensure metrics are calculated before sampling.

Let me explain.

Imagine your service emits 100 traces, and you have tail sampling configured at 25%. This means your Collector will
receive all 100 traces but will send approximately 25 to the observability backend.

If metrics are calculated in the same pipeline where data is exported, they'll reflect only about a quarter of the
total traces, resulting in significant information loss about your service.

To address this, you need to set up three pipelines:

* The first pipeline receives all spans from the traces and calculates its metrics.
* The second pipeline also receives all spans, but it samples the traces and exports only the sampled traces to the backend.
* The third pipeline receives the calculated metrics and exports them.

Here's an example setup:

```yaml
service:
  pipelines:
    traces/all:
      receivers: [otlp]
      exporters: [spanmetrics]
    traces/sample:
      receivers: [otlp]
      processors: [tail_sampling, resource, transform, batch]
      exporters: [debug, otlp]
    metrics:
      receivers: [otlp, spanmetrics]
      processors: [resource, transform, batch]
      exporters: [debug, otlp]
```

## It Keeps Going

This is a live, ongoing collaboration. Currently, I have a few open discussions with the Mastodon team, and with each
iteration, I learn more, and we work together to achieve a better observability state.

I hope this collaboration continues, as learning and growth are what truly motivate me.

To wrap up, I'd like to take this opportunity to thank Ara for this amazing onboarding experience, as well as Renaud
and Tim for all the back-and-forth discussions and the valuable insights I've gained from their use cases and questions.

[Ara Pulido]: https://www.linkedin.com/in/arapulido/
[Mastodon]: https://joinmastodon.org/
[Datadog's Open Source Hub]: https://opensource.datadoghq.com/projects/mastodon/
[source code]: https://github.com/mastodon/mastodon
[Robb Kidd]: https://github.com/robbkidd
[pull request]: https://github.com/mastodon/mastodon/pull/20338
[julianos-pr]: https://github.com/mastodon/mastodon/pull/29016
[Building a custom collector]: https://opentelemetry.io/docs/collector/custom-collector/
[Renaud Chaput]: https://oisaur.com/@renchap
[Tim Campbell]: https://mastodon.social/@timetinytim
[Inferred Services]: https://opensource.datadoghq.com/projects/mastodon/#inferred-services
[resourceprocessor]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/resourceprocessor/README.md
[transformprocessor]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/transformprocessor/README.md
[Reese Lee's presentation]: https://www.youtube.com/watch?v=l4PeclHKl7I
[Vijay and Aishwarya from eBay]: https://www.youtube.com/watch?v=RSJwv1jOdTg
[Tail-Based Sampling]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/tailsamplingprocessor/README.md
[spanmetricsconnector]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/connector/spanmetricsconnector/README.md
[datadogconnector]: https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/connector/datadogconnector
