---
title: "KubeCon Salt Lake City 2026: It's All About the Community"
date: 2026-11-23
draft: false
description: "Two talks, an OpenTelemetry Community Award and a red suit: my KubeCon Salt Lake City 2026."
tags: ["KubeCon", "OpenTelemetry", "OpenFeature", "Sampling", "Community"]
---

I came back from KubeCon Salt Lake City last week. Well, actually not last week: I got sick and stayed in bed for a week, but... Anyways, let's focus on the cool stuff. I want to talk about the community, and a couple of things that happened there that I'd like to share.

## Sharing the stage with the person who taught me sampling

This time I got two talks accepted. The first one was [Sample Smarter, Not Harder (Or Not At All!)](../../talks/Sample-smarter/index.md), together with Reese Lee.

This talk was really important to me. I actually learned sampling from Reese's talk at KubeCon Valencia (2022). So being on stage with her, talking about something I learned from her, was pretty great.

We went through a few different ways of reducing telemetry:

- **Uninstrumenting:** not really sampling, but dropping instrumentations that you don't need.
- **Probabilistic sampling.**
- **Tail sampling.**
- **Adaptive tail sampling**, something new we added to the talk.

Learning adaptive tail sampling was pretty cool. We struggled a bit with the configuration and everything, but I think that's what makes the talk valuable: we learned while preparing it, and we could deliver a nice talk. It was fun.

At the end we didn't get many questions, I think only two on the mic. But after the talk, some folks came to the front of the stage and we started chatting. We stayed there discussing different sampling scenarios and different configurations. For me, the best talks are the ones where people get engaged after the presentation, and that's what showed me this talk was actually valuable.

{{< figure src="img/kubecon-na-2026/after-talk.JPG" alt="Chatting with folks in front of the stage after the talk" caption="Chatting with folks after the talk" >}}

You can take a look at the slides, recording and repo in here if you would like: [Sample Smarter, Not Harder (Or Not At All!)](../../talks/Sample-smarter/index.md)

## Flipping switches on telemetry

My second talk was [OpenFeature as a Control Plane for OpenTelemetry](../../talks/OTelFeature/index.md), with Simon Schrottner. Simon is a maintainer on the OpenFeature side.

I usually give talks about OpenTelemetry, so sharing the stage with Simon, someone super knowledgeable on OpenFeature, was cool. I call this one kind of disruptive, because it changes the way we touch things in OpenTelemetry.

Usually, if you want to change the telemetry your app produces, you change some configuration and restart the application, or change the Collector configuration and restart the Collector. To deliver our talk, we hooked OpenTelemetry up with feature flags, so we could just flip switches in OpenFeature, and see different behaviors in the backend. No restarts. No redeploys. I really enjoyed this one.

You can take a look at the slides, recording and repo in here if you would like: [OpenFeature as a Control Plane for OpenTelemetry](../../talks/OTelFeature/index.md)

## An OpenTelemetry Community Award

Other than that, I got an [OpenTelemetry Community Award](https://opentelemetry.io/blog/2026/otel-community-awards/). The community nominates folks and then the maintainers vote, and this year there were five of us.

{{< figure src="img/kubecon-na-2026/community-awards.png" alt="2026 OpenTelemetry Community Award winners" caption="2026 OpenTelemetry Community Award winners" >}}

The nomination mentioned my work on the OTel Demo, docs and blog, and the DevEx SIG practitioner blog series, which ended up being the foundation for the reference implementation project. That was pretty cool. Thanks to everyone who nominated me and to the maintainers who voted.

Also, congrats to all other winners! You are all awesome!

## OpenTelemetry on the keynote stage

To celebrate OpenTelemetry's graduation, the community got together and put up a video that was shared on the main keynote stage. And yes, I was in it, so I got to see myself on a big screen, which was pretty cool.

{{< figure src="img/kubecon-na-2026/main-stage.JPG" alt="Me on the big screen during the keynote" caption="On the big screen at the keynote" >}}

OpenTelemetry wasn't the only one. There were a few projects graduating during KubeCon North America 2026, and it was nice to see all of them celebrated together.

{{< figure src="img/kubecon-na-2026/graduation.JPG" alt="All the projects graduating at KubeCon North America 2026" caption="The projects graduating at KubeCon NA 2026" >}}

## Some personal thoughts

At this KubeCon I met Leonardo Comelli, a former colleague from my time at HP, which later became DXC Technology. That was my first IT job.

He was one of the people responsible for sharing knowledge internally. This was around ten years ago, and he was already talking about containers and even Kubernetes. He was super into tech, and he still is. I saw him as an example and learned a lot from what he shared.

He also drove some initiatives internally to incentivize people to share what they were learning. Through it, I did a presentation with a friend on Java 8, the latest stable Java release at the time. Leo's team organized the sessions, scheduled the meetings and even took us to small conferences.

It's funny how things get aligned. In my first job, my role was making sure prod was working. When I left Brazil, back in 2017 I didn't know what would be the future, but it seems I got back to sharing knowledge.

I like to think that it's all connected to what started back then, so Leonardo has been really important in this journey and meeting him at KubeCon, where I was giving talks was gratifying.

{{< figure src="img/kubecon-na-2026/me-leo-addo.JPG" alt="With Leonardo and Addo at KubeCon" caption="With Leonardo and Addo at KubeCon" >}}

## Thank you

Two talks, two great co-speakers, a community award and meeting old friends. Thanks Reese, Simon, and everyone in the OpenTelemetry and OpenFeature communities I got to chat with.

See you at the next one!
