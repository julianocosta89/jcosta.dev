+++
title = 'KCD Austria 2024'
date = 2024-10-14
tags = [
    'wrapup',
    'Cloud Native',
    'CNCF Ambassador',
    'KCD Austria'
]
+++

KCD Austria 2024 was a blast!

I'm still trying to digest everything that happened last week.

I should probably start by admitting I’m biased in reviewing this event since I was part of the organizing team this year.
But hey, I’ll try to be as impartial as possible.

For the first time at KCD Austria, we hosted four workshops, and it was great to see the community already engaging a day
before the “main” event.

In between organizer duties, I managed to catch a few talks, and I’d like to share some highlights.

## Wednesday

We kicked off with a keynote from [Stefan Baumgartner][], who, in my opinion, is one of the best speakers I’ve ever seen.
Although he’s not from the Kubernetes/Cloud Native world, his talk on "failing successfully" was outstanding. He shared
their journey in allowing customers to securely run JavaScript code directly on the backend. The timing and tech jokes were
spot-on (as you can see in the photo below). I highly recommend checking out the recordings when they’re available.

![stefan-kcd](img/stefan-kcd.jpg
"Stefan Baumgartner keynote KCD Austria 2024 - Failing Successfully")

Then, the dilemma started...

With two tracks running simultaneously, we had to choose which talks to watch live, and which ones to watch later (whenever the
recordings are published). 😬

I decided to attend [Cleo Winkler][]'s talk, where she shared her research on the evolution and current state of inclusion
in IT, communities, and open source contributions. The biggest takeaway was the importance of simply “listening.” It’s a
must-see for every community builder worldwide. I hope to see this talk again at KubeCon.

![cleo-kcd](img/cleo-kcd.jpg
"Cleo Winkler - Cultivating Inclusion: Enhancing Diversity for a Stronger Kubernetes Community")

Next, I caught [Dominik Suß][]’s talk about why observability solutions need agents. He presented various deployment patterns
for managing telemetry data collection with the OpenTelemetry Collector. What I liked most was how he discussed both the
solutions and the challenges associated with each pattern.

After lunch, I attended the talk by [Josef Taha][], [Tobias Grantner][], and [Lukas Mahler][] on the Kubernetes Storm Center
project. Even though I’m not a security expert, I really enjoyed how they presented real-life threat exploits in a honey cluster.
It was fascinating stuff.

![tobias-lucas-josef-kcd](img/tobias-lucas-josef-kcd.jpg
"Tobias, Lukas and Josef - Kubernetes Storm Center: Open Source Threat Intelligence for Cloud Native")

Later, my fellow Datadog Tech Advocate, [Rory McCune][], shared key strategies for securing Kubernetes cluster management.
Though security isn't my specialty, Rory’s clear, well-structured points were very easy to follow.

![rory-kcd](img/rory-kcd.jpg
"Rory McCune - Fortifying Kubernetes - Strategies for Secure Cluster Management")

Unfortunately, I only caught the end of [Jose Javier Alonso Maya][] and [Fabrice Pipart][], who discussed the concept of
"Everything as Code." They covered everything from infrastructure as code to documentation and even slides as code.
Fun fact: I’m writing this blog post as code, so maybe they can include "blogging as code" in a future iteration of their talk. 🤭

![fabrice-jose-kcd](img/fabrice-jose-kcd.jpg
"Fabrice and Jose - Everything as Code: A Dozen As-Code Concepts beyond Infrastructure or Configuration as Code")

The day wrapped up with a closing keynote by [Lian Li][], who shared how her journey into art helped her realize that it’s all
about people and community. Even in IT, driven by data, it ultimately comes down to people.

![lian-kcd](img/lian-kcd.jpg
"Lian Li - In a Land Before Metrics: Embracing the Art of Uncertainty")

In the evening, we had the chance to connect and network with attendees, fellow organizers, and speakers at the event party.
It's amazing how such events allow you to connect with just about anyone. It’s just a matter of tapping someone on the shoulder
and starting a conversation.

One of the best parts was that these conversations ranged from highly technical topics, like the OpenTelemetry Collector distros,
to funny moments like discussing the fancy toilet in my hotel room. Seriously, it had all kinds of functions:

![toilet](img/toilet.jpg
"Fancy Toilet")

But don’t ask me how the conversation got there. 🙈 Hahaha

## Community

Though Pia’s keynote was on Thursday, I’m giving it its own section because it deserves a special focus.

On the third day, [Pia Gerhofer][] kicked off with a keynote about the power of community, building on the earlier themes from
Cleo’s and Lian’s talks. It was an excellent reminder of the importance of community, all the communities we have around Austria,
and I loved her shout-out to [Jakob][], part of the Cloud Native Linz community and one of the organizers of
[Linux / FOSS Meetup in Linz][]. It’s exciting to see new communities being created and people coming together to share and connect.

The previous night at dinner, someone asked me about my t-shirt, which had this quote: _“Viver é partir, voltar e repartir -
É tudo pra ontem”_. A direct translation to English would be: _“To live is to leave, return, and share - It is all for yesterday”_.

This quote comes from a song called _"É tudo pra ontem"_ by Emicida and Gilberto Gil:

{{< spotify src="https://open.spotify.com/embed/track/1FpjfHwVh1ziha91Ng2o4P?utm_source=generator&theme=0" >}}

To me, this captures what community is all about-caring, sharing, and the urgency of both. Pia highlighted the reasons why people
volunteer and organize within communities, and I’d like to add my own thoughts here:

> For me, it’s about giving back. I learn, I use, I share. We learn, we use, we share. The cycle continues.
>
> As part of the Cloud Native Linz and KCD Austria organizing teams, my goal is to provide a safe and welcoming space for people to
  share their stories, failures, and successes without judgment.
>
> I try to live by this philosophy, and I even have **UBUNTU** tattooed on my arm (not for the Linux distro by Canonical), but for
  its meaning. It is usually summarized as "I am because we are". For more, I recommend starting with the [Ubuntu philosophy][].

I’ll have to write a separate post on the power of community, but for now, let’s return to KCD.

## Thursday

After Pia’s keynote, [Joan Miquel Luque Oliver][] and [David Hondl][] talked about observability as code. I was especially excited
to see David, who previously presented at Cloud Native Linz. Their demo, showcasing Crossplane for configuring dashboards, alerts,
events and notifications, went smoothly. I also loved that my colleague [Tabitha Sable][] was referenced during their talk.

![david-joan-kcd](img/david-joan-kcd.jpg
"David and Joan - Observability as Code - DIY with Crossplane")

Later, [José Correia][] and [Iveri Pragishvili][] shared how they implemented DORA metrics in a Kubernetes cluster with 15,000
namespaces. Yes, you read that right, fifteen thousand namespaces. What I appreciated most was how they adapted the metrics to fit
their needs when the standard definitions didn’t quite fit their needs.

After lunch, my fellow CNCF Ambassador [Juraci Paixão Kröhling][] gave a keynote on my favorite topic: **Observability**. He walked
us through the evolution of software development and why observability is critical today. He also tackled some tough audience
questions, such as:

> Should I ditch monitoring in favor of observability?

I loved his response, he uses both. Monitoring helps track known issues, while observability helps investigate unknown unknowns.

![juraci-kcd](img/juraci-kcd.jpg
"Juraci Paixão Kröhling - The Role of Observability in Cloud Native Environments")

One personal highlight: As an OpenTelemetry Demo maintainer, I was thrilled to see a trace from the OTel Demo in Juraci’s presentation. 🤩

![otel-demo-kcd](img/otel-demo-kcd.jpg
"OpenTelemetry Demo")

The last talk I caught was from [Oleg Nenashev][], who gave an in-depth overview of observability in the Java stack. He covered
everything from Quarkus instrumentation to JVM metrics, though the pace was a bit fast for me. I’ll definitely re-watch the
recording to absorb all the details.

And I couldn’t resist mentioning [Dotan Horovits][], another CNCF Ambassador, who made his presence felt through Oleg’s talk, even
though he wasn’t there in person.

![oleg-kcd](img/oleg-kcd.jpg
"Oleg Nenashev - Modern Java app CI/CD observability with OTel, Quarkus and Gradle")

## Wrap-up

We spent over nine months organizing this event, and I’m extremely happy with how everything turned out. We’ll release more stats
and feedback later this month (October 2024), but for now, I want to extend my heartfelt thanks to the entire organizing team
(borrowing shamelessly from Constanze):

- [Johannes Grumböck][]: the mastermind who held everything together.
- [Henrik Rexed][]: who made it all observable, including the videos and interviews.
- [Andreas Taranetz][] and [Katharina Sick][]: for their outstanding work on the webpage, designs, and marketing.
- [Thomas Stagl][]: who coordinated the sponsors.
- [Erik Auer][]: for keeping our finances in check.
- [David Leitner][]: for organizing the scavenger hunt.
- [Daniel Drack][] and [Constanze Roedig][]: for hosting and making all the speakers feel welcome.
- [Andreas Grabner][]: who worked tirelessly on the overall organization and speaker coordination, though he couldn’t attend.

Thank you all for making this event so much fun, even when we were exhausted by the end of day three.

![kcd-fun](img/kcd-fun.jpg
"Daniel and I having some fun with the KCD's cube seats")

See you all next year, or maybe sooner at another community event!

[Stefan Baumgartner]: https://www.linkedin.com/in/stefan-baumgartner-bb621564/
[Cleo Winkler]: https://www.linkedin.com/in/cleo-winkler/
[Dominik Suß]: https://github.com/theSuess
[Josef Taha]: https://www.linkedin.com/in/joseftaha/
[Tobias Grantner]: https://www.linkedin.com/in/tobias-grantner/
[Lukas Mahler]: https://www.linkedin.com/in/lukas-mahler-6b83a71a1/
[Rory McCune]: https://www.linkedin.com/in/rorym/
[Jose Javier Alonso Maya]: https://www.linkedin.com/in/jjavieralonso/
[Fabrice Pipart]: https://www.linkedin.com/in/fabricepipart/
[Lian Li]: https://www.linkedin.com/in/lian-li/
[Pia Gerhofer]: https://www.linkedin.com/in/pia-gerhofer-29395719a/
[Jakob]: https://www.linkedin.com/in/jakob-hofer-simulatan/
[Linux / FOSS Meetup in Linz]: https://www.meetup.com/linux-foss-linz/
[Ubuntu philosophy]: https://en.wikipedia.org/wiki/Ubuntu_philosophy
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
