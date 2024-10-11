+++
title = 'KCD Austria 2024'
date = 2024-10-11
tags = [
    'wrapup',
    'Cloud Native',
    'CNCF Ambassador',
    'KCD Austria'
]
+++

KCD Austria 2024 was a blast!

I'm on the train back home trying to digest everything that happened in the last 3 days.

I should probably start by saying that I’m biased to do any type of review because
I was part of the organization this year, but hey, let me try to be as partial as possible.

For the first time in KCD Austria we had 4 workshops and it was great to see the community
already engaging 1 day before the “main” event.

Between one organizer task and another I had the chance to follow some talks and I’d like
to go through a couple of notes about it.

## Wednesday

We kicked off things with a keynote from [Stefan Baumgartner][], whom is, IMO, one of the best
speakers I’ve ever seen. He is not from the Kubernetes/Cloud Native world, but that didn't impact
his great talk on how to fail successfully. He went through their journey on how to allow customers
to run any javascript code directly on the backend securely. The talk had a great timing and
tech jokes all over (as we can see on the photo below), I’d recommend taking a look at the
recordings whenever they are available.

![stefan-kcd](img/stefan-kcd.jpg
"Stefan Baumgartner keynote KCD Austria 2024 - Failing Successfully")

After that the problem started...

We had 2 tracks, what is not much, but now we had to chose which talk to see live, and which one
to miss 😬.

I’ve checked [Cleo Winkler][] talk where she shared with us her research on the evolution and the
current state of inclusion in the IT world, communities and open source contributions. The main
takeaway that I’ll get home from her talk is to “Listen”. I’d say it is a must see to every
community builder all over the globe. I hope to see this talk again one day at KubeCon.

![cleo-kcd](img/cleo-kcd.jpg
"Cleo Winkler - Cultivating Inclusion: Enhancing Diversity for a Stronger Kubernetes Community")

Then I’ve checked out [Dominik Suß][]’s talk on why observability solutions need agents, presenting
us some deployments patterns to manage telemetry data collection with the OpenTelemetry Collector.
What I most liked about it was the fact that he showed solutions and problems to each of the patterns.

After lunch I joined @Josef Saha, @Tobias Grantner and @Lukas Mahler, on their talk about
the Kubernetes Storm Center project. Even though I’m not a security person I really enjoyed
how they presented the project with some real life threat exploit in a honey cluster. Really cool stuff.

![tobias-lucas-josef-kcd](img/tobias-lucas-josef-kcd.jpg
"Tobias, Lukas and Josef - Kubernetes Storm Center: Open Source Threat Intelligence for Cloud Native")

Then my fellow Datadog Tech Advocate, [Rory McCune][], shared some key strategies to secure
k8s cluster management. Again, I’m not a security person, but I loved how well Rory stated
his points and was clear about each strategy.

![rory-kcd](img/rory-kcd.jpg
"Rory McCune - Fortifying Kubernetes - Strategies for Secure Cluster Management")

Unfortunately I was only able to get the end of the talk from [Jose Javier Alonso Maya][]
and [Fabrice Pipart][] on everything as code. It was pretty impressive that they went from most common
stuff like, infrastructure as code to documentation and even slides as code. A fun fact on that is
that I'm writing this blog post as code, so maybe they can add blogging as code in a next iteration
of the talk 🤭.

![fabrice-jose-kcd](img/fabrice-jose-kcd.jpg
"Fabrice and Jose - Everything as Code: A Dozen As-Code Concepts beyond Infrastructure or Configuration as Code")

To wrap up the day we had [Lian Li][] with a closing keynote sharing how her journey into art helped
her to understand that it’s all about people/community. Even in IT, where we are driven by data,
in the end, it’s all about people.

![lian-kcd](img/lian-kcd.jpg
"Lian Li - In a Land Before Metrics: Embracing the Art of Uncertainty")

In the evening we had the chance to connect and network with attendees, other organizers and
speakers at the event party. It is fascinating how such events help you connect with
basically everyone you want to. It is just matter of tapping someone on the shoulder and start chatting.

The best part of it is that those conversations go from super technical topics like Juraci, Dominik,
and I discussing the OpenTelemetry Collector and its distros, to really funny things like the fancy
toilet I had in my hotel room. Like, literally fancy, it wasn't made of gold, but it had all those
functions:

![toilet](img/toilet.jpg
"Fancy Toilet")

Just don't ask me how the conversation got there. 🙈 Hahaha

## Community

Pia's keynote was on Thursday, but as I've spent a lot of time talking about it, I've decided to break
it down to it's own section.

The 3rd day started with [Pia Gerhofer][] talking about community. This adds another layer to the
community cake we were building till now with Cleo’s and Lian’s talks. Such a great talk sharing
the power of the community and all the communities we have around Austria. I personally loved
her mentioning [Jakob][] in the talk, because he is part of the Cloud Native Linz community and has
been running, together with some friends, the [Linux / FOSS Meetup in Linz][]. It is great to
see the community expanding and people getting together to share and connect.

During the evening dinner, the day before, someone asked me what was written on my t-shirt, and
it was that: _“Viver é partir, voltar e repartir - É tudo pra ontem”_. A direct translation to English
would be: _“To live is to leave, come back and share - It is all for yesterday”_.

This is from a song called _"É tudo pra ontem"_ by Emicida and Gilberto Gil:

{{< spotify src="https://open.spotify.com/embed/track/1FpjfHwVh1ziha91Ng2o4P?utm_source=generator&theme=0" >}}

Basically that is what community is all about, caring and sharing, and this is urgent, we need that
for yesterday. Pia shared some reasons why volunteers and organizers are involved in their communities,
and I'd like to add my own testimony here.

> To me, it's all about giving back to the community. I learn, I use, I share. We learn, we use, we share.
  And the cycle goes on.
>
> As part of the Cloud Native Linz and KCD Austria organizer's team, my personal goal is to provide a
  safe place to people to share their stories, their failures, their successes without being judged and
  feeling welcomed by the whole community.
>
> I honestly try to live that. I have **UBUNTU** tattooed in my arm, and it is not because of Canonical's
  linux distribution (as a lot of people ask me), but because what it means. It is not easy to explain a
  philosophy in one sentence, but usually Ubuntu is translated as: "I am because we are".
  If you want to know more, I'd recommend starting with the wiki article about it: [Ubuntu philosiphy][].

I think I'll have to write a blog post focused on the power of the community and how being part
of those communities helped me personally and professionally, but let's get back to KCD.

## Thursday

After the keynote, [Joan Miquel Luque Oliver][] and [David Hondl][] talked about observability as code,
but before going to the talk itself I’d like to say I’m happy to see David here, as he already
presented at the Cloud Native Linz. I’m always excited to see community members stepping up to bigger
stages, keep it going David! The demo gods were with them while they presented the steps to configure
dashboards, alerts, notifications and events, using Crossplane.
Also I loved to see my fellow Datadog colleague [Tabitha Sable][] being quoted there.

![david-joan-kcd](img/david-joan-kcd.jpg
"David and Joan - Observability as Code - DIY with Crossplane")

Later, [José Correia][] and [Iveri Pragishvili][] presented how they implemented DORA metrics in an
k8s cluster with 15000 namespaces, and nope, it is not a typo, you read it correctly.
Fifteen thousand namespaces.

What I liked about this one, is that they took the definition, applied it, and then noticed that the
way it was defined didn't work for them, so they adjusted it to have an extra metric that was
meaningful for them.

After lunch we had my fellow CNCF Ambassador [Juraci Paixão Kröhling][] in a keynote session talking
about my favorite topic in the Cloud Native landscape: **Observability**. Juraci drove us through the
evolution of software development to reach the state we are today, and how important is Observability.
He also took some tricky questions from the audience like:

> Should I ditch monitoring in favour of Observability?

And I loved how he explained that he uses both. Monitoring to keep track of issues that already happened,
can happen again and overall state of the system. And Observability whenever unknown unknowns raise and
he needs to explore his telemetry to find reasons why the application is having this unexpected
behavior.

![juraci-kcd](img/juraci-kcd.jpg
"Juraci Paixão Kröhling - The Role of Observability in Cloud Native Environments")

Before moving on, I want to call out one thing that made me happy before Juraci even started his talk.

If you know me, I guess you know that I'm one of the maintainers of the OpenTelemetry Demo, and I
think you already know where I'm going, but if not, let me explain. Juraci had a screenshot on his cover
slide, this screenshot was a trace from the OpenTelemetry Demo 🤩.

![otel-demo-kcd](img/otel-demo-kcd.jpg
"OpenTelemetry Demo")

The last talk I was able to follow was from another fellow CNCF Ambassador, [Oleg Nenashev][] where
he went through all the steps to have observability in the whole Java stack, going through Quarkus
instrumentation, JVM metrics with OTel Java agent and a hell lot of manual configuration if you want
to have CI observability.

I have to confess, he was a bit too fast for me, I'll definitely re-watch the talk whenever the recordings
go live because he touched a lot of great concepts there.

And I couldn't let it pass that, even though [Dotan Horovits][] (another fellow CNCF Ambassador) wasn't there,
he made his way to the KCD Austria with Oleg.

![oleg-kcd](img/oleg-kcd.jpg
"Oleg Nenashev - Modern Java app CI/CD observability with OTel, Quarkus and Gradle")

## Wrap-up

We have been working for more than 9 months to deliver the event. I'm extremely happy to how
things went through and with the feedback I got from the community during the event itself.

We will release all the stats and feedback later this month (October, 2024), but for now I just want to
thank every single one of the organizer's team (stealing shamelessly from Constanze):

- [Johannes Grumböck][] the mastermind who kept it all together.
- [Henrik Rexed][] who made it observable and without whom we wouldn't have these videos, nor the interviews.
- [Andreas Taranetz][] and [Katharina Sick][] who did an incredible job on the webpage, the designs and marketing materials.
- [Thomas Stagl][] who coordinated the sponsors.
- [Erik Auer][] who kept all finances in order.
- [David Leitner][] who organized the scavenger hunt.
- [Daniel Drack][] and [Constanze Roedig][] who were hosts in the rooms and made all speakers feel welcome.
- [Andreas Grabner][] who worked with general organization and with the speakers, but unfortunately wasn't able to join the event.

Thanks everyone and thanks for taking time to have fun, even when everyone was tired by the end of the 3rd day.

![kcd-fun](img/kcd-fun.jpg
"Daniel and I playing with the KCD's cube seats")

See you all next year, or maybe earlier in one of the community events around.

[Stefan Baumgartner]: https://www.linkedin.com/in/stefan-baumgartner-bb621564/
[Cleo Winkler]: https://www.linkedin.com/in/cleo-winkler/
[Dominik Suß]: https://github.com/theSuess
[Rory McCune]: https://www.linkedin.com/in/rorym/
[Jose Javier Alonso Maya]: https://www.linkedin.com/in/jjavieralonso/
[Fabrice Pipart]: https://www.linkedin.com/in/fabricepipart/
[Lian Li]: https://www.linkedin.com/in/lian-li/
[Pia Gerhofer]: https://www.linkedin.com/in/pia-gerhofer-29395719a/
[Jakob]: https://www.linkedin.com/in/jakob-hofer-simulatan/
[Linux / FOSS Meetup in Linz]: https://www.meetup.com/linux-foss-linz/
[Ubuntu philosiphy]: https://en.wikipedia.org/wiki/Ubuntu_philosophy
[Joan Miquel Luque Oliver]: https://www.linkedin.com/in/joanluque/
[David Hondl]: https://www.linkedin.com/in/david-lastnamenotfoundexception/
[Tabitha Sable]: https://www.linkedin.com/in/tabithasable/
[José Correia]: https://www.linkedin.com/in/jmmcorreia/
[Iveri Pragishvili]: https://www.linkedin.com/in/iverip/
[Juraci Paixão Kröhling]: https://www.linkedin.com/in/jpkroehling/
[Oleg Nenashev]: https://www.linkedin.com/in/onenashev/
[Dotan Horovits]: https://www.linkedin.com/in/horovits/
[Johannes Grumböck]: https://www.linkedin.com/in/jgrumboe/
[Henrik Rexed]: https://www.linkedin.com/in/hrexed/
[Andreas Taranetz]: https://www.linkedin.com/in/andreas-taranetz/
[Katharina Sick]: https://www.linkedin.com/in/katharinasick/
[Thomas Stagl]: https://www.linkedin.com/in/thomas-stagl/
[Erik Auer]: https://www.linkedin.com/in/erik-auer/
[David Leitner]: https://www.linkedin.com/in/leitner-david/
[Daniel Drack]: https://www.linkedin.com/in/drackthor/
[Constanze Roedig]: https://www.linkedin.com/in/croedig/
[Andreas Grabner]: https://www.linkedin.com/in/grabnerandi/
