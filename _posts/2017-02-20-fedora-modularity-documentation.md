---
id: 340
title: Fedora Modularity Documentation
date: 2017-02-20T11:39:10+00:00
author: adam
guid: http://blog.samalik.com/?p=340
permalink: /fedora-modularity-documentation/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6181831913"
categories:
  - Fedora
  - Modularity
---
Wiki pages are great for collaboration. But they are not that great in getting people&#8217;s attention. They can also become pretty messy and hard to navigate trough when using multiple pages that are related to each other &#8211; like documentation &#8211; which was what we had there. We needed something better. Something that would make it easy to go trough multiple pages of documentation. Something that would have a simple landing page explaining what we do. And having a simple way to review the changes people make before publishing them would be also great.

I knew we wanted something better, but I didn&#8217;t know what exactly. I also didn&#8217;t want to invent yet another way to build docs. So I looked around, and found the <a href="https://docs.pagure.org/releng/" target="_blank">Fedora Release Engineering documentation</a>. It&#8217;s hosted in <a href="https://docs.pagure.org/pagure/usage/using_doc.html" target="_blank">Pagure Docs</a>, it&#8217;s built with <a href="http://www.sphinx-doc.org/" target="_blank">Python Sphinx</a>, and it also used to be a wiki. And I got inspired!

So I created some drafts, made a proposal, and convinced people from the <a href="https://fedoraproject.org/wiki/Modularity_Working_Group" target="_blank">Modularity Working Group</a> that we need a cool website. And then I just built it. Using the same tech as the Fedora Release Engineering team &#8211; Python Sphinx to build, Pagure Docs to host.

But because I&#8217;m a wanna-be designer, I also created a logo, and wrote a custom Sphinx template including a simple landing page that helps people quickly understand what Modularity is about.

**And I&#8217;m happy to announce that the <a href="https://docs.pagure.org/modularity" target="_blank">new Fedora Modularity documentation website</a> has been published today!**

To edit the documentation, please send pull-requests against our <a href="https://pagure.io/modularity" target="_blank">source repository</a>. And maybe get in touch if you like the project!
