---
id: 397
title: Flock 2017 was awesome!
date: 2017-09-12T11:48:44+00:00
author: adam
guid: http://blog.samalik.com/?p=397
permalink: /flock-2017-was-awesome/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6184141413"
categories:
  - Fedora
---
<a href="https://flocktofedora.org/" target="_blank">Flock</a> is a <a href="https://getfedora.org/" target="_blank">Fedora</a> contributors&#8217; conference happening every year, alternating between the US and Europe. And this year it was a more action-oriented than in previous years which means there were more workshops and &#8216;do-sessions&#8217;, and less talks.

I must admit I liked that change because I think that presenting a project online is easier than quick discussions and getting things done online. So using this even with many people together to do stuff as opposed to presentations seems pretty effective.

I was there to represent the <a href="https://docs.pagure.org/modularity/" target="_blank">Fedora Modularity</a> effort &#8211; giving two and a half talks, collecting feedback and ideas, and learning from awesome people.

[<img class="aligncenter size-large wp-image-409" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/cape-1024x455.png" alt="cape" width="600" height="267" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/cape.png)

## Day one

### Keynote

Matt Miller talked about the current state of Fedora. There are many changes going on, and it&#8217;s a good thing. We don&#8217;t want to be completely on fire, but also not super stable because we want to innovate. So the answer is: Just a little bit of fire. Matt had the following chart on [his slides](https://mattdm.org/fedora/2017flock/2017-State-of-Fedora.pdf) showing what our audience is.[<img class="aligncenter size-large wp-image-400" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/blog-flock-keynote-1024x362.png" alt="blog-flock-keynote" width="600" height="212" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/blog-flock-keynote.png)

And this chart is what I took from the keynote. Doing innovation means braking stuff. And that&#8217;s fine as long as we keep it under control.

### Advertise your session

Everyone got a chance to sell their presentations or workshops to others before the conference began. There was a long line of people and everyone was introducing themselves and their presentation or workshop to others. Interesting idea, I liked the concept, there were just so many people I was loosing track a little bit. My proposal for next time: could we group them by topic? What do you think?

### User Feedback on Modularity

This was a bit special event, as it was running six times during the conference! Two slots every day, an hour before lunch, and an hour after lunch. This fact alone felt like Modularity is pretty important to Fedora.

And it was also important to the Modularity people. We got a lot of feedback &#8211; both nice and useful. Every single one liked the overall concept of Modularity, majority also liked the UX.

[<img class="aligncenter size-thumbnail wp-image-403" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/IMG_4004-150x150.jpg" alt="IMG_4004" width="150" height="150" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/IMG_4004.jpg)

One of the things I liked was that every day was a little bit different. Why? Because we had Martin Hatina &#8211; a DNF developer &#8211; with us. And he was fixing the code every day as people were discovering little bugs!

### Factory 2.0, Fedora, and the Future

Mike Bonnet gave an intro into the Factory 2.0 project, giving an overview of all the new and old services that are part of that project and that are being worked on. It was a verygood presentation, also serving as an introduction to other, more detailed talks the team was giving, as he provided a high-level overview of everything that&#8217;s going on in Factory, and pointed us to the other talks for more details.

He gave an introduction into the following projects:

  * **Module Build Service (MBS)** &#8211; A service for building modules in Fedora.
  * **Arbitrary Branching** &#8211; Naming branches to follow upstream version of the component instead of a Fedora release.
  * **ResultsDB **&#8211; Test results from the infrastructure on a single place.
  * **WaiverDB **&#8211; Allowing tests to be waived, turning a fail into a pass.
  * **Greenwave **&#8211; Gating for content to move to a new state &#8211; like pushing updates automatically.
  * **Bodhi** &#8211; Package (and now also module) updates in Fedora. Gating on Greenwave decisions now deployed!
  * **Freshmaker **&#8211; Automatically triggers builds of content when its source gets updated.
  * **ODCS **&#8211; On-demand Compose Service, generates repos of signed pre-release content to build other content like containers, ostrees, and to run tests.

### State of Fedora Server

Stephen Gallagher talked about the history, current state, and the future of Fedora Server Edition.

People could learn that previously, there was just a single Fedora &#8216;edition&#8217; designed to run on a laptop and on a server. And that was fine then, but later on, both groups started to have different needs &#8211; like different defaults on a fresh system. On a laptop, you probably want to have a window manager &#8211; like Gnome &#8211; running. On a server, you might want a different GUI to manage it remotely, like Cockpit. And that&#8217;s why they split the Server Edition and the Workstation Edition apart.

And that is very nice! When you install a fresh Fedora Server, it has Cockpit running by default. That means you can just open your web browser on your laptop, log in to your server, and you&#8217;ll be able to see all the logs, CPU and memory consumption, and to perform basic configuration like managing your LVM volumes. Thanks to Cockpit apps you are (or will be in some cases) also able to manage other services like your containers or the FreeIPA server.

While the Server and Workstation split enabled this, there are still needs like having multiple versions available or independent lifecycles of some components. And that&#8217;s where Modularity comes in. Modularity enables parallel availability of content &#8211; so people will be able to choose different versions of software to install, or even the Server WG will be able to choose different default (even with a different lifecycle) for the Server as opposed to the Workstation. During the discussion, someone mentioned that Modularity is like customizing a laptop. You can choose the color, the CPU &#8211; but you can only fit one, etc. And I liked that. It was also nice to see people who are not &#8216;us&#8217; to understand Modularity well enough to explain it to others.

### Proposal: Splitting docs from the software

This was my first talk. I gave a short introduction into the problem of having the software and the documentation in a single source. This also applies to tests. Right now, to build a package, you need to have all the build requires for your software, for the documentation, and for the tests. That grows the build dependencies a lot which is a problem with Modularity where we want to be as flexible as we can &#8211; so having many build dependencies lowers the flexibility. That&#8217;s a problem especially for the base which hould have as little build dependencies as possible. Texlive or python-sphinx might be a nice example.

After the short introduction, we had a discussion about how we could solve that problem. I proposed two solutions: having a standard macro in SPEC that could switch the documentation off, or separating docs from the software on a source level. There are advantages to both: the first one is easier to maintain, as you have just a single thing. Also, the version of the docs will always match the version of the software. The drawbacks are that you need to rebuild the SRPM with the correct macros to get the right build requires. The second option is easier for build, because you have two separate things.

I was lucky enough to have Jason Tibbitts from the Fedora Packagibg Comittee in the discussion. And we decided to go with the second option &#8211; separating docs from the software on a source level for the critical components. However, we won&#8217;t force anyone to do that. Instead, we will explicitly mention in the packaging guidelines that this is absolutely fine, and recommended for some components, and then we&#8217;ll ask maintainers of the core components to do the change.

## Day two

### How to write dist-git tests in Fedora with Ansible

Stef Walter believes that lot of work in the future will be done by robots! And that includes testing our packages. Tests for the CI.. I mean.. robots can be described using Ansible.

I learned that you can work in two scenarios:

  * setting up the environment like VMs or containers for the tests to run in
  * setting up the environment like VMs or containers as part of the tests

Learn more: http://fedoraproject.org/wiki/Changes/InvokingTests

### Freshmaker

Jan Kaluza makes automation happen! He presented the project he works on called Freshmaker, that automatically makes fresh things. It is a service that triggers rebuilds of content on a source change. It will make packagers&#8217; life easier by removing many manual steps from their workflow.

The short-term goal for Freshmaker is to:

  * trigger container rebuilds when an RPM source changes
  * trigger module rebuilds when a modulemd changes

### Gating on automated tests in Fedora &#8211; Greenwave

Matt Jia talked about Greenwave &#8211; a service that makes clever decisions about pushing content to another stage based on test results (consumed from ResultsDB and WaiverDB) and policy. This, for example, will enable pushing updates in Bodhi automatically, based on transparent criteria.

### Atomic Host 101

OK, I&#8217;m lying. I wasn&#8217;t really here. But Dusty made an awesome job with the worshop and made it available online with all the instructions you need. And it&#8217;s completely offline! Once you download all the bits and pieces, you can play with it anywhere. So I tried it on the way back home. You should try it, too!

The most impressive thing was changing the OS from Fedora to CentOS with a single command, and everything worked fine after a reboot. Go for it:

  * <a href="https://dustymabe.com/2017/08/29/atomic-host-101-lab-part-0-preparation/" target="_blank">Atomic Host 101 Lab Part 0: Preparation</a>
  * <a href="https://dustymabe.com/2017/08/30/atomic-host-101-lab-part-1-getting-familiar/" target="_blank">Atomic Host 101 Lab Part 1: Getting Familiar</a>
  * <a href="https://dustymabe.com/2017/08/31/atomic-host-101-lab-part-2-container-storage/" target="_blank">Atomic Host 101 Lab Part 2: Container Storage</a>
  * <a href="https://dustymabe.com/2017/09/01/atomic-host-101-lab-part-3-rebase-upgrade-rollback/" target="_blank">Atomic Host 101 Lab Part 3: Rebase, Upgrade, Rollback</a>
  * <a href="https://dustymabe.com/2017/09/02/atomic-host-101-lab-part-4-package-layering-experimental-features/" target="_blank">Atomic Host 101 Lab Part 4: Package Layering, Experimental Features</a>
  * <a href="https://dustymabe.com/2017/09/03/atomic-host-101-lab-part-5-containerized-and-non-containerized-applications/" target="_blank">Atomic Host 101 Lab Part 5: Containerized and Non-Containerized Applications</a>

### The Future of fedmsg?

Jeremy Cline explained the current state of fedmsg, the problems they&#8217;re having with it, and a possible solution.

Right now, when using fedmsg, you basically need to subscribe everything to everything. And the messages are not guaranteed to be delivered.

The most interesting for me was a discussion about guaranteed vs. not guaranteed messaging. Basically, when you have a guaranteed message bus, it makes things very complicated. The sender needs to know about all the receivers. So you can no longer just consume the messages as you can now with fedmsg. Also, you can&#8217;t entirely trust the message broker, so you need to have a code in your app to handle this anyway. It seemed to me that building a reliable messaging bus might not be worth it.. but is it the right answer? I dont&#8217; know.. but it&#8217;s pretty interesting problem and got me thinking about that for sure.

### Evening Activity @ Wackenhammer&#8217;s Clockwork Arcade and Carousel

It was very relaxing, good fun, here&#8217;s a picture of me winning a 1000 tickets, and let&#8217;s move on!

[<img class="aligncenter size-thumbnail wp-image-401" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/arcade-150x150.jpg" alt="arcade" width="150" height="150" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/09/arcade.jpg)

## Day three

The Modularity day! We had four hours in the afternoon. So let&#8217;s start.

### Modularity &#8211; the future, building, and packaging

Join session of Langdon White, Ralph Bean, and me. We got a full room!

**Langdon** talked about the vision, why are we doing it, and some of the benefits it brings. He talked about the F26 Boltron Server we have built, the F27 Server MVP we are currently working on, about building Atomic as rolling updates separated from the other editions which is now work in progress, and about Workstation using Flatpaks in the future.

One of my favourites was a demonstration how to build container images with multiple versions of things without changing the dockerfile. See <a href="http://Join session of Langdon, Ralph, and me. We got a full room!" target="_blank">Langdon&#8217;s slides</a> for the example. He also emphasized how we want to make packagers&#8217; life as easy as possible, mostly by generating many of the things and running tests in the infrastructure.

**Ralph** gave us update on the Module Build Service (MBS) &#8211; a service that builds modules in Fedora. It is for developement and production. MBS runs in the Fedora infrastructure and orchestrates builds in Koji, but the same thing can also run on your laptop and use Mock to do your local builds. That means they share the code-base between the infra and the client tool which is a good thing.

We could also learn how MBS reuses components. There is a concept of build groups people can define in their modulemd. And basically all the builds get reused if their buildroot (which is the previous build group) haven&#8217;t changed. It&#8217;s very nicely explained in <a href="http://threebean.org/presentations/mbs-flock17/" target="_blank">Ralph&#8217;s slides</a> &#8211; so have a look!

And finally, in **my part** I talked about packaging. I explained the difference between traditional distribution, where packages have a branch for every release, and releases are built out of these branches; and the modular distro, where we have arbitrary branching, multiple version of content, and we use modulemd to describe the builds and the modules produced out of it.

I also talked about an idea of defining spins and editions using modulemd files. See <a href="https://www.slideshare.net/Adamamalk/packaging-modularity-flock-2017" target="_blank">my slides</a> for more details and a bunch of graphics!

### When to go fully modular?

This was a discussion about the future of Modularity. During the session I realized I should have advertised it as a Fedora Modularity WG meeting live. That would have been awesome. So maybe next time.

**How many modules will be there?**

A module could be described as a group of packages with additional metadata. But how bit is the group? Do we create a &#8216;text-editors&#8217; module, do we create &#8216;vim&#8217;, &#8216;nano&#8217;, &#8217;emacs&#8217;, and others? And should they include all the dependencies, or shoud the dependencies be shared between modules? The result is that we want to do the later, a module per application or service. And that they should share the dependencies.

But how to share the dependnecies? In a huge &#8216;shared-userspace&#8217; module? Or using many small modules? And how to coordinate all of this so the modules won&#8217;t overlap? The outcome wasn&#8217;t that clear this time. The consensus was that creating smaller sensible modules as dependencies instead of &#8216;shared-userspace&#8217; is probably better. But how small do we want to go? Do we want to push it to the extreme and have modules with a single package? And what about the overlaps and coordination?

Flatpaks and containers make this much easier, as they can overlap with each other by design. But installing RPMs directly on a system makes it difficult. We will need a service that will help packagers to coordinate. Something similar to the dependency-report I have prototoyped, but as a service, and focusing on the long-term maintenance over one off migration.

**Is there an everything else module?**

There are basically two main approaches how to modularize a distro:

  1. Build a huge &#8216;everything else&#8217; module and separate individual modules out of it as we go. This way, we would have all the content.
  2. Modularize everything &#8211; including dependencies &#8211; from the start. We wouldn&#8217;t have all the content from the beginning, but it would be much cleaner. And we could get rid of some packages that are no longer maintained, but are being automatically rebuilt over and over again.

Someone also had an idea to include the traditional Fedora Everything repo in the modular distro to give users the content. However, it would conflict with the modularized packages, and could also have binary incompatibilities. That was clearly a bad idea. But what about the everything \_else\_ module?

I think most of the people would go with the option 2, modularize everything. And that&#8217;s what we do with the F27 Server.

**How could we do Rawhide in Modularity?**

That was an interesting question. Also, how do we do releases in the pure modularity world? Will we have a releases as we know them now? Or will individual modules (or module stacks) have their own releases? Would we have a rawhide as we know it today, for the whole distro, or will modules have their own &#8216;rawhide&#8217; streams? We haven&#8217;t agreed on this one.

**How do we deal with module EOL?**

When every module and every RPM can have independent EOL (end of life), it can turn into a pretty messy situation when something can expire any time. And that&#8217;s not good. Matt Miller proposed we have a standardized EOL dates, for example every 6 months. That way, it would be basically the same as we have now, except some RPMs and modules could live longer. And that was the consensus in the end.

### Let&#8217;s create a module

Tomas Tomecek did a workshop for packagers where they could build their module and see the whole process from the beginning to the end. It&#8217;s availabe on github: <a href="https://github.com/fedora-modularity/workshop" target="_blank">Modularity Workshop</a>.

### Let&#8217;s create tests for modules/containers

Petr Hracek and Jan Scotka explained people how to use the Meta Test Family to write tests for modules. It supports writing tests in any framework and running them in any environment. More information here: <a href="https://github.com/fedora-modularity/meta-test-family" target="_blank">Meta Test Family</a>.

## Day four

### What did we do / Demo day

People had a chance to present what they have achieved during the conference. It was interesting to see what other people learned and got done. As a side-effect, it helped me remember some of the things I have been part of myself. Even though there was a bit pressure in the end asking people to come and speak, I think it was just because people were not used to this sort of thin on previous Flocks. I believe that next year the pressure will disappear as more people will be getting ready for this during the week. I still think it was useful and I liked it.

## Wrap-up

It was awesome. I believe that just meeting people face to face is so important, as it makes the collaboration for the upcoming year so much easier when people know each other. Besides the sessions, I had many hallway (and pub) discussions. I liked seing other people to understand Modularity well enough they could explain it to others. I liked getting all the feedback and great ideas &#8211; especially the little ones, that were part of the hallway discussions. I liked the positive perception of Modularity on the UX demos. I learned a bunch of new stuff, met some new people I haven&#8217;t known in person before.

Thank you for having me there, it was very useful and pleasant experience!

&nbsp;
