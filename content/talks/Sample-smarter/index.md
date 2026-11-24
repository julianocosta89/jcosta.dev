+++
title = 'Sample Smarter, Not Harder (Or Not At All!)'
date = 2026-11-11
description = "Sample Smarter, Not Harder (Or Not At All!)."
tags = [
    'OpenTelemetry',
    'Sampling',
    'KubeCon'
]
+++

Think sampling is just about reducing your vendor bill? Think again! 

The truth is, the cost of telemetry starts way before it reaches your backend. It starts inside the application process itself, and increases the farther it goes before it’s sampled in your OTel Collector or backend.

In this session, we reframe sampling as a performance and cost strategy that spans the entire telemetry pipeline. We start with application-level overhead and see how different language SDKs can impact performance, and why sometimes the answer isn’t better sampling; it’s not instrumenting at all.

We’ll use the OTel demo app, Astronomy Shop, as our live environment to explore the sampling decision hierarchy, including declarative config to drop known-noisy signals, when to use head- or tail-based sampling, probabilistic sampling, and more.

Join our talk to connect business outcomes to concrete instrumentation and configuration decisions, and for an honest take on where sampling helps and where it doesn’t.

{{< youtubeLite id="PSobbPLsbak" label="Play: Sample Smarter, Not Harder (Or Not At All!)" >}}

Slide deck:

{{< gslides src="https://docs.google.com/presentation/d/e/2PACX-1vQ9vqQx9iNnEdxBMbmxYFe9VolvLhJlzblFlVt_i4IL5cSeADjK7-El9Ef1j76j-3qYO1PqxGOTsZLj/embed" >}}

[Github repo with examples](https://github.com/julianocosta89/kubecon-na-2026)
