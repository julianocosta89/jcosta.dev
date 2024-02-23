+++
title = 'Getting Started with OpenTelemetry: OTel Demo to the Rescue'
date = 2024-02-22
tags = [
    'OpenTelemetry',
    'Cloud Native St. Pölten',
    'Developer Advocate'
]
+++

On the 22nd of February we held our [1st Cloud Native St. Pölten meetup][st-polten-meetup].

The event was hosted by [Cloudflight][cloudflight] and had about 15 people.
It wasn't a large event, but it was definitely an engaging one.

With not that many attendees, everyone is more comfortable asking questions and interacting with each other.

After the presentation I got questions like:

- "Given that OpenTelemetry is a project that is still evolving (with Profiling being added and new
signals eventually arriving), how does the project work to ensure the OpenTelemetry protocol will
not undergo breaking changes?"
  - To answer this one, I actually got help from the community itself, [João Grassi][joao-grassi]
    and [Sebastian Poxhofer][sebastian-poxhofer] were there and jumped in to discuss how the backwards
    compatibility and interoperability are core parts of the [OpenTelemetry Protocol (OTLP) Specification][otlp-spec].
  - Just a side note here, I love meetups and how we all grow together in those events.
  Thanks João and Sebastian for jumping in.
- Another question was, "When you auto-instrument your application, how do you add business related attributes to it?"
  - To answer this, I jumped into the IDE and shared the OpenTelemetry Demo code for 2 services:
    - [adservice][adservice] in Java, which simply retrieves the current automatically created span
    and adds custom attributes to it:

    ```java
    Span span = Span.current();

    [...]

    span.setAttribute("app.ads.count", allAds.size());
    span.setAttribute("app.ads.ad_request_type", adRequestType.name());
    ```

    - [quoteservice][quoteservice] in PHP, in which we manually create a new child span
    and add attributes to it:

    ```php
    $childSpan = Globals::tracerProvider()
        ->getTracer('manual-instrumentation')
        ->spanBuilder('calculate-quote')
        ->setSpanKind(SpanKind::KIND_INTERNAL)
        ->startSpan();

    [...]

    $childSpan->setAttribute('app.quote.items.count', $numberOfItems);
    $childSpan->setAttribute('app.quote.cost.total', $quote);

    [...]

    $childSpan->end();
    ```

    - Both approaches showcase how we can leverage OpenTelemetry (OTel) to add business context
    to our instrumentation, demonstrating the flexibility and power of OTel in enhancing observability
    with custom data relevant to our specific business needs.

As I’ve mentioned before, it was a really engaging event, and although I can't recall all the questions
asked, another one I’d like to highlight is directly related to my talk:

- "We have a microservices architecture with about 150 microservices, how do we start?"
  - This question came up after all the talks had finished, during a discussion on
  troubleshooting methods when issues arise. At the moment, they rely on logs and are kind of used to
  this approach.

    I guess this is also true for a lot of companies where developers are just used to logs.

    Thankfully they saw how powerful the correlation between signals can actually help them
    troubleshooting issues and were interested in getting to know more about OTel.

Just the spark of curiosity, the eagerness to learn more, and the willingness to start experimenting
OpenTelemetry made the event immensely worthwhile for me.

My goal as a Developer Advocate focused on OpenTelemetry and Distributed Tracing is to raise awareness
of the project and assist people in starting their journey with ease.

Events like these meetups are an excellent opportunity to engage deeply with the community, and
I’m grateful for being an organizer of Cloud Native Linz myself.

Thanks [Thomas Schuetz][thomas-schuetz] and [Daniel Drack][daniel-drack] for organizing and having me on the event.

Also, a big thank you to everyone who joined and engaged; the event was great because of each one of you!

Slide deck:

{{< gslides src="https://docs.google.com/presentation/d/1bcMdC7Coz0gAeBxbByVrudyspqS9GL5e33Nv9MpMPTY/embed" >}}

[st-polten-meetup]: https://www.meetup.com/cloud-native-austria/events/298751920/
[cloudflight]: https://www.cloudflight.io/en/
[joao-grassi]: https://github.com/joaopgrassi
[sebastian-poxhofer]: https://github.com/secustor
[otlp-spec]: https://github.com/open-telemetry/opentelemetry-proto?tab=readme-ov-file#opentelemetry-protocol-otlp-specification
[adservice]: https://github.com/open-telemetry/opentelemetry-demo/blob/main/src/adservice/src/main/java/oteldemo/AdService.java
[quoteservice]: https://github.com/open-telemetry/opentelemetry-demo/blob/main/src/quoteservice/app/routes.php
[thomas-schuetz]: https://github.com/thschue
[daniel-drack]: https://github.com/DrackThor
