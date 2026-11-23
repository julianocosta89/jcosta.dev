+++
title = "KubeCon Salt Lake City 2026: It's All About the Community"
date = 2026-11-23
# TODO: add featured.jpg to this folder, add after-talk.jpg (see below), then set draft = false
draft = true
description = 'Two talks, an OpenTelemetry Community Award and a red suit: my KubeCon Salt Lake City 2026.'
tags = [
    'KubeCon',
    'OpenTelemetry',
    'OpenFeature',
    'Sampling',
    'Community'
]
+++

I came back from KubeCon Salt Lake City last week, but I got sick on my way home and stayed in bed for a week with fever and everything. It was tough. But that's not what this post is about. I want to talk about the community, and a couple of things that happened there that I'd like to share.

## Sharing the stage with the person who taught me sampling

This time I got two talks accepted. The first one was [Sample Smarter, Not Harder (Or Not At All!)](https://github.com/julianocosta89/kubecon-na-2026), together with Reese Lee.

This talk was really important to me. I actually learned sampling from Reese's talk at KubeCon Valencia, around four years ago. So being on stage with her, talking about something I learned from her, was pretty great.

We went through a few different ways of reducing telemetry:

- **Uninstrumenting:** not really sampling, but dropping instrumentations that you don't need.
- **Probabilistic sampling.**
- **Tail sampling.**
- **Adaptive tail sampling**, something new we added to the talk.

Learning adaptive tail sampling was pretty cool. We struggled a bit with the configuration and everything, but I think that's what makes the talk valuable: we learned while preparing it, and we could deliver a nice talk. It was fun.

At the end we didn't get many questions, I think only two on the mic. But after the talk, some folks came to the front of the stage and we started chatting. We stayed there discussing different sampling scenarios and different configurations. For me, the best talks are the ones where people get engaged after the presentation, and that's what showed me this talk was actually valuable.

<!-- TODO: drop the photo into this folder as after-talk.jpg -->
{{< figure src="after-talk.jpg" alt="Chatting with folks in front of the stage after the talk" caption="Chatting with folks after the talk" >}}

## Flipping switches on telemetry

My second talk was [OpenFeature as a Control Plane for OpenTelemetry](https://otelfeature.dev/), with Simon Schrottner. Simon is a maintainer on the OpenFeature side.

I usually give talks about OpenTelemetry, so sharing the stage with Simon, someone super knowledgeable on OpenFeature, was cool. I call this one kind of disruptive, because it changes the way we touch things in OpenTelemetry.

Usually, if you want to change the telemetry your app produces, you change some flags and restart the application, or change the Collector configuration and restart the Collector. We hooked OpenTelemetry up with feature flags, so we could just focus on the scenarios, flip switches in OpenFeature, and see different behaviours in the backend. No restarts. I really enjoyed this one.

## An OpenTelemetry Community Award

Other than that, I got an [OpenTelemetry Community Award](https://opentelemetry.io/blog/2026/otel-community-awards/). The community nominates folks and then the maintainers vote, and this year there were five of us.

The nomination mentioned my work on the OTel Demo, docs and blog, and the DevEx SIG practitioner blog series, which ended up being the foundation for the reference implementation project. That was pretty cool. Thanks to everyone who nominated me and to the maintainers who voted.

## My first KubeCon in red

It was also my first KubeCon as a Dash0 person, so I had the chance to wear the red suit. At every event the Dash0 folks go full red suit, like a Formula One pit crew. I didn't present with it, but I walked around a bit and spent some time wearing it.

## Thank you

Two talks, two great co-speakers, a community award and a red suit. Thanks Reese, Simon, and everyone in the OpenTelemetry and OpenFeature communities I got to chat with.

See you at the next one!
