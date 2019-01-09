---
id: 355
title: Modularity update – sprint 31
date: 2017-06-07T12:26:25+00:00
author: adam
guid: http://blog.samalik.com/?p=355
permalink: /modularity-update-sprint-31/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6194094301"
categories:
  - Fedora
  - Modularity
---
Hello people of the world! Let me give you another update of the <a href="https://docs.pagure.org/modularity" target="_blank">Fedora Modularity</a> project.

## What we did

We are moving the modules to the new <a href="https://github.com/modularity-modules" target="_blank">Fedora Modularity: modules</a> space on GitHub. All work regarding modules will be done primarily here and synced into <a href="http://pkgs.fedoraproject.org/cgit/modules/" target="_blank">fedora dist-git</a> for builds. Each module has its own repository with an **issue tracker.**

The <a href="https://docs.pagure.org/modularity/docs.html" target="_blank">Modularity <strong>documentation</strong></a> has been **updated** and slightly restructured.

There is also a new <a href="https://www.youtube.com/watch?v=pxh-C5fDDaU" target="_blank">demo about the dnf prototype</a> supporting modules on our <a href="https://www.youtube.com/channel/UC4O8G9SZwqtkIAuKcT8-JpQ" target="_blank">YouTube channel</a>.



### Try the DNF prototype

You can try everything you have seen in the video yourself! We have a container image with everything you need to get started. See the <a href="https://github.com/container-images/dnf-modularity-prototype" target="_blank">DNF Modularity Prototype repository</a> for the source, or get the image directly from Docker hub:

<pre>$ docker pull jamesantill/flat-modules-dnf</pre>

Then start a container using this image with an interactive shell:

<pre>$ docker run --rm -it jamesantill/flat-modules-dnf /bin/bash</pre>

Now, when you are in the container, you can try all the commands. And please give us feedback either in the comment section below, in the <a href="https://github.com/container-images/dnf-modularity-prototype/issues" target="_blank">issue tracker</a>, or get in touch on the <a href="http://IRC channel" target="_blank">#fedora-modularity freenode channel</a>.

## What’s next?

  * Complete all modules, images, and tests.
  * Prepare an example and a demo of multiple streams of NodeJS.
  * Review and prioritize open issues.
