---
id: 36
title: 'Copr update &#8211; new features in July 2014'
date: 2014-07-31T12:20:10+00:00
author: adam
guid: http://blog.samalik.com/?p=36
permalink: /copr-update-new-features-in-july-2014/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6627650230"
categories:
  - Copr Build Service
  - Fedora
---
<a title="Copr is an easy-to-use automatic build system providing a package repository as its output." href="http://copr.fedoraproject.org/" target="_blank">Copr</a> is an easy build service for <a title="Fedora is a Linux-based operating system that showcases the latest in free software. Fedora is always free for anyone to use, modify, and distribute. It is built by people across the globe who work together as a community: the Fedora Project." href="http://fedoraproject.org/" target="_blank">Fedora</a> which can make you your own repo very easily. I have been contributing to this project since March 2014 and this month has been the best in terms of new features: you can track your builds much better, it is bit easier to use and also got much faster in some cases.

## Build detail &#8211; packages and versions

This is a quite new view showing all the information about your build progress and results. This month&#8217;s new feature is the Build packages section &#8211; which shows you names and versions of the result packages which has been built.

<img class="aligncenter wp-image-39 size-full" src="http://blog-shaman.rhcloud.com/wp-content/uploads/2014/07/build-detai.png" alt="build-detai;" width="809" height="860" />

## API extension &#8211; build details

The same information as above is also available via API. Have a look at <a href="http://copr.fedoraproject.org/api/" target="_blank">some more details about Copr API</a>.

## Overview page &#8211; modified buildroots and generated dnf command

Two new things has been added to the project&#8217;s overview page &#8211; one of which could help you when building <a title="Software Collections's Collections" href="https://www.softwarecollections.org/en/scls/user/rhscl/?page=1" target="_blank">Software collections</a>.

Have you found a project with packages added to the minimal buildroot and want to see a list of them? There is a new button for it: [modified]

And if you decide that you want this repo enabled in your system, just copy the dnf command to your terminal.

<img class="aligncenter size-full wp-image-43" src="http://blog-shaman.rhcloud.com/wp-content/uploads/2014/07/overview.png" alt="overview" width="792" height="807" />

## Bit of speeding up

There are some mass rebuilds of loads of packages in which just some have changed since last time. Copr is now able to skip the unchanged packages almost immediately as I moved this process out of Mockremote &#8211; the build script- to the beginning of the worker process. This means massive speed-up in some cases.

## New build states &#8211; skipped and starting

If you build a package successfully and some time later you submit the very same one again, it gets skipped. This saves your time and Copr&#8217;s resources, because there is no need of doing the same thing again. And from now on it would be marked as Skipped instead of Succeeded to make it more transparent.

The other state is an intermediate step while spawning a builder. It happens between picking up from the queue and the building process itself.

&nbsp;
