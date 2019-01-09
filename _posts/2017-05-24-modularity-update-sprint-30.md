---
id: 347
title: 'Modularity update &#8211; sprint 30'
date: 2017-05-24T14:07:10+00:00
author: adam
guid: http://blog.samalik.com/?p=347
permalink: /modularity-update-sprint-30/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6227961996"
categories:
  - Fedora
  - Modularity
---
The <a href="https://docs.pagure.org/modularity" target="_blank">Fedora Modularity</a> team already publishes sprint reports on the <a href="https://www.youtube.com/channel/UC4O8G9SZwqtkIAuKcT8-JpQ" target="_blank">Modularity YouTube channel</a> every two weeks. But this format might not be always suitable &#8211; like watching on a phone with limited data. So I would like to start writing short reports every two weeks about Modularity, so people have more choice of how to get updated.

## What we did

  * We have the **<a href="https://github.com/fedora-modularity/boltron-content-tracking" target="_blank">final list of modules we are shipping in F26 Boltron</a>**. The list shows Python 2 and Python 3 as not-included which is not entirely true. Even thought we won&#8217;t be shipping them as separate modules due to various packaging resons, they will be included in Boltron as part of the Base Runtime and shared-userspace.
  * One of them is **shared-userspace** which is a huge module that contains common runtime and build dependencies with proven ABI stability over time. Lesson learned: building huge modules is hard. We might want to create smaller ones join them together as a module stack.
  * To **demonstrate** **multiple streams **we will include NodeJS 6 as part of Boltron, and NodeJS 8 in Copr &#8211; built by its maintainer.
  * The DNF team has implemented a [**fully functional DNF version that supports modules**](https://copr.fedorainfracloud.org/coprs/mhatina/DNF-Modules/).
  * We have **changed** the way we do demos on **YouTube**. Instead of posting a demo every two weeks of work per person, we will do a sprint review + user-focused demos as we go. I will also do my best with writing these posts. 🙂

## What&#8217;s next?

**Modules**:

  * clean up and make sure they deliver the use cases we promised
  * the same for containers if time allows

**Documentation and community:**

  * issue tracker for each module
  * revisiting documentation
  * revisiting how-to guides

**Demos**:

  * we would love to make a demo based on a working compose (if we get a qcow)

Also, **I&#8217;m going to Zagreb to give a [Modularity talk at DORS/CLUC](https://2017.dorscluc.org/talk/12/) next week**. Come if you&#8217;re near by! 😉
