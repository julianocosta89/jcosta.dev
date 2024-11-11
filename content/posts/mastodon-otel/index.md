+++
title = 'Mastodon & OpenTelemetry'
date = 2024-10-28
tags = [
    'OpenTelemetry'
]
+++

I joined Datadog in January this year (2024), and in February, [Ara Pulido][], a colleague of mine, connected me with [Mastodon][]
to help onboard their backend to Datadog.

They were using Datadog as part of the Open Source Program Datadog offers to Open Source projects for an year already, mainly
to monitor their hosts, kubernetes cluster, logs and database performance, but they were looking into OpenTelemetry to get some
visibility into their backend.

I wrote about it on [Datadog's Open Source Hub][], but I wanted to add some personal/technical points to this process that
didn't fit the Open Source Hub post, so here it goes.

## Initial Challenges

When I started looking at the [source code][], I noticed that Mastodon is written in Ruby. Although, I've touched Ruby in
my previous work, it is totally different creating a sample Ruby app, from a real world application, but thankfully it worked
out fine.

The community had already started working on something similar. [Robb Kidd][] sent a [pull request][] back in November
2022 to add OTel to Mastodon, and I've built on top of that a solution [shipping the OTel Collector with it][julianos-pr].

## The PR with the Collector

Even though this wasn't the PR that got merged, I'd like to spend a minute here to discuss one nice thing that I suggested.

### The Collector

As Mastodon wanted to allow users to send telemetry data to any observability backend, I wanted to build a minimal collector,
containing just the components required for each vendor, and each developer would configure their Collector in their own way.

To do that, I've used a multi-staged Dockerfile which first would use the OCB (OpenTelemetry Collector Builder) to build a
minimal Collector distro based on a manifest file that specifies which components should be part of the Collector distro. And
then runs the Collector with its configuration file.

Here is how a `manifest.yaml` file looks like:

{{% snippet manifest.yaml yaml %}}

This is how the `Dockerfile` would look like:

{{% snippet Dockerfile Dockerfile %}}

And finally, here is how the `otelcol-config.yaml` file would look like:

{{% snippet otelcol-config.yaml yaml %}}

{{< alert >}}
Note that you can only use the components previously added to the manifest file, as the custom Collector has only
those components. If you try to use a component that is not defined in the manifest the Collector will fail to start.
{{< /alert >}}

If you want to know more about the OCB, you can take a look at the official OpenTelemetry docs: [Building a custom collector][].

### The Instrumentation

The main difference between the initial PR from Robb and mine in the instrumentation side, was that instead of using the
`opentelemetry-instrumentation-all`, I suggested adding only the dependencies we need.

This is way more verbose and requires more maintenance, but we have more control over what we are instrumenting. This also
aligned with the idea behind building a minimal Collector distro.

We don't import everything automatically, we define what we want, what we need, and only use those.

## The Collector Configuration

After the PR from the Mastodon team got merged, [Renaud Chaput] and [Tim Campbell] started
sending OpenTelemery traces to Datadog via Collector.

In here it started a great back and forth between them and I that I'll be forever grateful.

I represent the community/users/customers inside Datadog, and hearing exactly what are their pain
points and troubles when sending OTel data to Datadog is one of the most important part of my job.

In the [Datadog's Open Source Hub] blog post I've spent some time talking about [Inferred Services]
and how that improved Mastodon's usability significantly.

In here, I want to focus on some Collector configuration that helped them navigate better the
OTel world in Datadog.

### Resource Processor

In the snippet below, the [resourceprocessor] component is used to set an attribute
`deployment.environment.name=development`.

When the OTel data arrives at Datadog with that attribute, the service is tagged with the
defined value, and that makes their life easier when navigating the data in Datadog.

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

Working with the [transformprocessor] was a great learning to me. I knew the existence of the component,
but I have never used it myself.

Mastodon wanted some help to get a better naming to their spans, other than the default Ruby instrumentation name.

They would like to have the values from `code.namespace` be merged with `code.function`. If you don't know
what a code namespace and function are, as I didn't, let me show you an example.

A namespace would be something like `Api::V1::Timelines::PublicController` and the function `show`.

The snippet below concatenates those two values with a `#` in between, resulting in this:
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
Note that we are actually not changing the span name, but rather setting the resource name.
This is a Datadog concept that we do not need to explore here, but if you are interested, you can
take a look at the [Resources glossary](https://docs.datadoghq.com/tracing/glossary/#resources).
{{< /alert >}}

### Tail Sampling Processor

I remember as if it was today the [presentation from Reese Lee] about [Tail-Based Sampling] at KubeCon
EU 2022. It was my first contact with the concept and I was pretty impressive by its power. Reese also
nailed the presentation with some live hands-on.

Another talk that I have to mention is from [Vijay and Aishwarya from eBay] in this year's (2024) Observability
Day EU, where they blew my mind when said that they sample just 1% of their traces, as that percentage is
enough for their traffic volume 🤯.

Tail sampling has a catch when you use multiple Collectors, where you have to make sure all spans from
a trace reaches the same Collector, otherwise you will have some broken traces.

In Mastodon's case though, I got lucky because they are using a single instance of the Collector, which
made our life configuring it way easier.

Initially I've suggested 25% of sampling, plus all errors, but Tim was already satisfied with 10% plus errors.

Below we have the `tail_sampling` processor definition for this.

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

Another point to highlight about tail sampling is that if you calculate metrics from spans
with components such as the [spanmetricsconnector] or [datadogconnector], you have to make sure
the metrics are being calculated before the sampling.

Let me elaborate a bit on that.

Imagine your service emits 100 traces and you have a tail sampling configure to 25%.
That means that your Collector will receive 100 traces, but it will send to the observability backend
approximately 25 traces.

If you calculate the metrics in the same pipeline you export the data, the metrics will be calculated
with a quarter of its total, and you will miss a lot of information about your service.

To solve this, you have to use three pipelines:

* The first one receives all spans from the traces and calculate the metrics of it;
* The second one also receives all spans, but it samples the traces and exports only
  the sampled traces to the backend;
* The third one receives the calculated metrics and exports them.

Here is an example of it:

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

That's a live collaboration which is still ongoing. At the moment I have a couple of opened discussions
with the Mastodon's team and in every iteration I learn more and we reach a better observability state.

I hope that keeps going, because learning and growing is what motivates me.

To wrap it up, I just want to take the chance to publicly thank Ara for this awesome onboarding gift.
As well as Renaud and Tim for all the back and forth and everything that I learnt from their use-cases
and questions.

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
[presentation from Reese Lee]: https://www.youtube.com/watch?v=l4PeclHKl7I
[Vijay and Aishwarya from eBay]: https://www.youtube.com/watch?v=RSJwv1jOdTg
[Tail-Based Sampling]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/tailsamplingprocessor/README.md
[spanmetricsconnector]: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/connector/spanmetricsconnector/README.md
[datadogconnector]: https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/connector/datadogconnector
