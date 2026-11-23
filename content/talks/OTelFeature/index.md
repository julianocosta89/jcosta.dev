+++
title = 'OpenFeature as a Control Plane for OpenTelemetry'
date = 2026-11-12
description = "OpenFeature as a Control Plane for OpenTelemetry."
tags = [
    'OpenTelemetry',
    'OpenFeature',
    'KubeCon'
]
+++

Most observability configurations are static. 

We decide upfront which spans to emit, which attributes to record, and how much telemetry is worth collecting. But production systems are not static. When everything is healthy, detailed telemetry creates unnecessary cost and noise. When incidents happen, the telemetry we need often is not being collected.

What if telemetry verbosity could adapt automatically?

In this talk, we combine OpenTelemetry and OpenFeature to dynamically control instrumentation at runtime. Services can switch between lightweight traces and deep diagnostic telemetry without redeployments or restarts. Feature flags drive observability decisions based on runtime conditions, enabling richer spans, additional attributes, and higher-cardinality signals only when they are needed.

We will demonstrate how OpenTelemetry semantic conventions can act as a standardized control surface, enabling adaptive and vendor-neutral observability across services and environments.

{{< youtubeLite id="tvc7MmpJ82Y" label="Play: OpenFeature as a Control Plane for OpenTelemetry" >}}

Slide deck:

{{< gslides src="https://docs.google.com/presentation/d/e/2PACX-1vTakjXEJNaAThzRYjtxw-pcc5Gt-_KHJvDmYPg7_rkTHdWJvbZ11S9KLx-EG5YUwCHpsLBwMil0ZFMV/embed" >}}
