---
title: Flock to Fedora 2019 report
---

I loved being at [Flock](https://flocktofedora.org/) this year!

Flock is an annual Fedora conference for contributors, this year happening in Budapest, Hungary. What I loved about the venue this year was the single hallway space for discussions, and talk being in rooms around that space. It was a very productive and pleasant conference to be at! I've met many people I haven't seen for a while, learned about bunch of stuff, and discussed next steps for various initiatives in Fedora I'm being a part of.

## Minimization

Presented my talk about the [Minimization Objective](https://flock2019.sched.com/event/SJZP/an-objective-minimization-objective-update) and I think it went fine. I also met a few people who are interested in the initiatives and have a few interesting conversations. It was great to see that almost everyone thought it's an important and useful thing to do, touching the whole Fedora ecosystem.

Many people have already been doing similar work since a long time ago — playing Whack a Mole with random dependencies. This initiative should give them some better tools to play with, and some automated checks that make sure that when you whack a mole once, it won't pop out again and if it does, it sends a notification.

## IoT

I attended three talks about IoT. One by Peter Robinson titled [Fedora IoT: who, what, when, where, why, how?](https://flock2019.sched.com/event/SJUt/fedora-iot-who-what-when-where-why-how) that explained IoT in a general way including some details I haven't realised before. The other by Chad Ferman titled [Deploying Fedora IoT in an enterprise, a discussion of the trials and tribulations](https://flock2019.sched.com/event/SKtH/deploying-fedora-iot-in-an-enterprise-a-discussion-of-the-trials-and-tribulations) which was a practical example of trials of deploying Fedora IoT in an industrial focused enterprise in a quite massive scale. And finally, a talk by Patrick Uiterwijk titled [Fedora IoT Security features](https://flock2019.sched.com/event/SKrN/fedora-iot-security-features) that explained how to secure a device that people can have a physical access to. Patrick covered everything from secure boot and verification at all the steps up to the application code, including securing information on the device in case the device itself is stolen or manipulated with.

I learned about IoT, including the big difference between Fedora IoT and Fedora CoreOS. They're both rpm-ostree-based releases focusing on servers, but the key difference is in the details. While CoreOS is targeting cloud and data centres — with fast network connections and an ability to terminate broken instances and just re-spin new ones, IoT is targeting single devices out in the fields — with often very slow network connections, without the data centre security, and especially without the ability to just terminate broken instances and re-spin new ones — it's a single device. It's like the difference between your sofa and an airplane seat — they're both for sitting, but have very different requirements.

IoT is quite related to Minimization and the two groups will be working together.

## Modularity

There were [three Modularity-related events at Flock]() two of which I've lead or helped leading. Both were quite interactive, and we've clarified things and collected issues.

The initial discussion titled [Modularity: to modularize or not to modularize](https://flock2019.sched.com/event/SJd1/modularity-to-modularize-or-not-to-modularize) I've organised was targeted at a wider audience with the goal to discuss broader topics. I started with a short presentation and then we dived into various topics for discussion. Thanks Stephen Gallagher for helping me lead the discussion! We talked about streams, parallel installation, and a few specific cases that Modularity can or can not solve, providing existing alternatives in the latter case. We ended up with two issues the Modularity tracker regarding [Module API](https://pagure.io/modularity/issue/146) and [dependency resolution](https://pagure.io/modularity/issue/147).

I heard Merlin Mathesius did a good job with his [Tools for Making Modules in Fedora](https://flock2019.sched.com/event/SDo9/tools-for-making-modules-in-fedora) which I couldn't attend because I had a conflict.

Finally, we did the [Modularity & packager experience birds-of-a-feather](https://flock2019.sched.com/event/SJL4/modularity-packager-experience-birds-of-a-feather) which was a two-hour discussion about various topics. We've time-boxed the initial brainstorming of issues, and then dived deep into 4 that got the most votes, giving every topic about 15-20 mins and writing down the next action that needs to be done to resolve the issue. We ended up with 5 flip charts in the end covering modules in buildroot, building modules by third parties using existing build processes and systems such as OBS and Copr that [Stephen Gallagher has already written about](https://sgallagh.wordpress.com/2019/08/14/sausage-factory-modules-fake-it-till-you-make-it/), offline local builds, and module upgrades.

## Fedora Magazine

I've also quickly discussed a new editorial workflow for the Fedora Magazine with Ben Cotton, making it more so that we have a separate process for submitting proposals and ideas, and a queue of approved "article specs" for anyone to pick and write. More will be coming soon!

