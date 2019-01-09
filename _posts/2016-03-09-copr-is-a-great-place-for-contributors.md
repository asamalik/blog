---
id: 247
title: Copr is a great place for contributors
date: 2016-03-09T14:54:33+00:00
author: adam
guid: http://blog.samalik.com/?p=247
permalink: /copr-is-a-great-place-for-contributors/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6188198688"
categories:
  - Copr Build Service
  - Fedora
---
We have recently moved our code to <a href="https://github.com/fedora-copr/copr" target="_blank">GitHub</a>, and we support a local development environment using Vagrant &#8211; which means, that collaboration have never been easier. Even if you&#8217;re very new to the world of open source, this might be a good place for you to start. For example, an easy fix of a typo might be a great opportunity for you to make your first open source contribution! 🙂

## What is Copr?

<a href="https://copr.fedoraproject.org/" target="_blank">Copr</a> is a community build service in Fedora that builds your code and provides you with your own RPM repository.

[<img class=" wp-image-249 size-medium alignnone" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2016/03/copr-workflow-300x96.png" alt="Source code is builded in copr and an RPM repository is created." width="300" height="96" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2016/03/copr-workflow.png)

So, if you are a developer, you can build your application in Copr and make it available for everyone. Or you might be packager &#8211; a person, who creates packages of open source software, which are easy to install in Fedora. Then you have two options:

  1. Make the package a part of the Fedora distribution using <a href="https://fedoraproject.org/wiki/Packaging:Guidelines" target="_blank">Fedora Packaging Guidelines</a>. If your package passes a review and all the formal requirements, the package will be added to Fedora and you will become an owner of the package. This means, that you will be responsible for making updates and reporting issues to the upstream, or fixing them. You will become an appreciated member of the Fedora community! 🙂
  2. Build the package in Copr. This option requires less commitment, and it is also suitable for testing or quick and dirty solutions. In fact, it&#8217;s totally up to you to decide the quality of your packages and how often you will update them. Copr is a build service for everyone. <a href="https://developer.fedoraproject.org/deployment/copr/about.html" target="_blank">Learn more about using Copr.</a>

## Local development environment with Vagrant

Vagrant can create a local development environment on your workstation. It is very easy to use and will not break your environment, as it installs everything in virtual machines.

### Starting the environment

<pre>$ git clone https://github.com/fedora-copr/copr.git
$ cd git
$ vagrant up</pre>

This spawns two virtual machines on your workstation:

  1. Copr Frontend &#8211; including the web interface and database &#8211; http://localhost:5000
  2. Copr Dist Git &#8211; storage for the source code &#8211; http://localhost:5001

_(optional)_ If you want to start only one specific virtual machine, run one of these commands:

<pre>$ vagrant up frontend
$ vagrant up distgit</pre>

### Testing your changes

To test your changes, commit them to your local repository and reload the virtual machines.

Example:

<pre>$ git add .
$ git commit -m "changed something really important"
$ vagrant reload frontend</pre>

This will restart the Copr Frontend virtual machine, rebuild your package and install it.

### Accessing the virtual machines

If you need to access the virtual machines, you can use either:

<pre>$ vagrant ssh frontend
$ vagrant ssh distgit</pre>

### Rebuilding broken virtual machines

Have you destroyed one of the machines completely? That&#8217;s fine! To delete it and install it again from the scratch, use:

<pre>$ vagrant destroy frontend
$ vagrant up frontend</pre>

You can do the same for _distgit_ as well.

### Stopping the virtual machines

<pre>$ vagrant halt</pre>

## Contributing

Now, when you know what Copr is, how to make changes, and you maybe did some experiments, you are ready to change the world! Well, make a pull-request to the Copr project.

To find out what specifically needs to be done, visit our <a href="https://bugzilla.redhat.com/buglist.cgi?bug_status=NEW&bug_status=ASSIGNED&bug_status=POST&bug_status=MODIFIED&bug_status=ON_DEV&bug_status=ON_QA&bug_status=VERIFIED&bug_status=RELEASE_PENDING&classification=Community&list_id=4754450&product=Copr&query_format=advanced" target="_blank">bugzilla</a>. Or ask on our <a href="https://lists.fedorahosted.org/admin/lists/copr-devel.lists.fedorahosted.org/" target="_blank">mailing list</a>.

You should also familiarize yourself with pull-requests. You will need to:

  1. <a href="https://help.github.com/articles/fork-a-repo/" target="_blank">fork</a> our project
  2. create a <a href="https://help.github.com/articles/using-pull-requests/" target="_blank">pull-request</a>

And that&#8217;s it! If you have any questions about Copr, contributing, or anything related to this article, please leave a comment in the comment section below. I&#8217;m looking forward to hear from you!

## Useful resources

  * Copr Build Service: <https://copr.fedoraproject.org>
  * Project page: <https://fedorahosted.org/copr/>
  * Git repository: <https://github.com/fedora-copr/copr>
  * Bugzilla: [Copr Bugzilla](https://bugzilla.redhat.com/buglist.cgi?bug_status=NEW&bug_status=ASSIGNED&bug_status=POST&bug_status=MODIFIED&bug_status=ON_DEV&bug_status=ON_QA&bug_status=VERIFIED&bug_status=RELEASE_PENDING&classification=Community&list_id=4754450&product=Copr&query_format=advanced)
