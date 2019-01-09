---
id: 167
title: Copr, Dist Git and Patternfly
date: 2015-07-19T11:17:24+00:00
author: adam
guid: http://blog.samalik.com/?p=167
permalink: /copr-dist-git-and-patternfly/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6186718003"
categories:
  - Copr Build Service
  - Fedora
  - User Interface
---
As in the last year, July, for some reason, happened to be a great time to post some news about our [Copr Build Service](http://copr.fedoraproject.org). At this time, it&#8217;s about integrating Copr with:

  * [Patternfly](http://www.patternfly.org) &#8211; an open interface project
  * [Dist Git](https://github.com/release-engineering/dist-git) &#8211; a remote Git repository designed to hold RPM package sources

_If you can&#8217;t wait to see it, you can check [the development server](http://copr-fe-dev.cloud.fedoraproject.org/) that is hopefully running on [copr-fe-dev.cloud.fedoraproject.org](http://copr-fe-dev.cloud.fedoraproject.org/). But please, remember, it&#8217;s a development server &#8211; so all the projects built here are a subject of deletion, destruction and all kinds of randomization without notice._

### Dist Git for Copr

It all started with a need of **uploading sources** to the Copr itself &#8211; as the only way of building your package was to provide a URL pointing to it. That, however, required all users to have their own public file storage.

We decided to go the Fedora way and use [Dist Git](https://github.com/release-engineering/dist-git) &#8211; a combination of git repository to store spec files, lookaside cache to store sources, and Gitolite to manage access permissions. Each package will be stored in a repo named as &#8216;username/project/package&#8217;. Each repo will contain branches that represent a target platform. For example: &#8216;f22&#8217; for Fedora 22, &#8216;epel7&#8217; for Epel for Centos 7, etc.

<img class="aligncenter" src="https://github.com/release-engineering/dist-git/raw/master/images/storage.png" alt="" width="1592" height="1150" />

It will be gradually deployed in production. The first step is to **enable users to upload their .src.rpm** files into Copr. At this step, Dist Git will be used as a storage only. Direct access to the repositories will come afterwards.

### New User Interface  Patternfly

Enabling Dist Git required some changes to the user interface as well. We didn&#8217;t use any framework, that would help us to easily create new elements in the UI. Instead, we had a custom CSS that received new lines of code with each change. As you can imagine, each change took a bit longer than desired, the CSS became messy, and yes, the interface itself became messy as well. At this point, I decided that we need to do a step forward and we finally agreed to rewrite the user interface to [Patternfly](https://www.patternfly.org/)! Yay!

#### The Old Copr UI

[<img class="alignleft wp-image-181 size-large" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2015/07/old-copr1-819x1024.png" alt="The old Copr interface" width="600" height="750" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2015/07/old-copr1.png)

#### The New Copr UI

[<img class="alignleft wp-image-182 size-large" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2015/07/new-copr1-1024x872.png" alt="The new Copr interface" width="600" height="511" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2015/07/new-copr1.png)

### We need your feedback!

I would like to make Copr as friendly as possible. If you want to help me with that, please provide a feedback as a comment. Do you like it? Do you hate it? Is there anything you miss in the interface? Your feedback is much appreciated!
