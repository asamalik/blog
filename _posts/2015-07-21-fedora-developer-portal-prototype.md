---
id: 154
title: 'Fedora Developer Portal &#8211; prototype'
date: 2015-07-21T15:14:06+00:00
author: adam
guid: http://blog.samalik.com/?p=154
permalink: /fedora-developer-portal-prototype/
catchflames-sidebarlayout:
  - default
categories:
  - Fedora
---
I wanted to try an interesting project called Jekyll &#8211; a static page generator. It consumes content in textual form like Markdown or Textile, Liquid templates, and HTML and CSS to generate static pages and blogs.

I should be able to install it with simple command:

<pre>$ <span class="command">gem install jekyll</span></pre>

But it wasn&#8217;t successful. What I&#8217;m going to do?

Good news for me is that I work on a project called Fedora Developer Portal! And there is a [repo for content](https://github.com/developer-portal/content/) with the Ruby section already created. It explains how to install Ruby, Gems, etc. I used that information and successfully installed Jekyll on my machine.

That&#8217;s one of the purposes of our new portal &#8211; to help people start with new (new for them) technology on Fedora.

### First Prototype is Here!

As you might have figured out from the introduction, and from the heading as well, the development slowly started! I just finished a [prototype](https://developer-phracek.rhcloud.com/) which is running on [developer-phracek.rhcloud.com](https://developer-phracek.rhcloud.com/).

Please keep in mind that this is just a prototype that offers very limited content and functionality. The content is not final and will change according to your feedback and ideas 🙂

### Project Resources

#### General Information

  * [Wiki page](https://fedoraproject.org/wiki/Websites/Developer) &#8211; The main project page with description, links to resources, planning etc.

#### Code & Development

  * [Content repo](https://github.com/developer-portal/content) &#8211; Repo with all the content in a textual form with Markdown syntax. (Ruby content already created)
  * [Website repo](https://github.com/developer-portal/website) &#8211; Repo for Jekyll templates that would define the visual look and layout of the website.
  * [Design mockups repo](https://github.com/developer-portal/mockups) &#8211; Repo for layout sketches and mockups.
  * [Prototype](https://developer-phracek.rhcloud.com/) &#8211; Prototype of the website with limited content and functionality.

#### Communication

  * [Taiga Project](http://taiga.cloud.fedoraproject.org/project/fedora-developer-portal/kanban) &#8211; Project tracking and planning
  * IRC channel #developer-portal on Freenode
  * Issue Trackers in the GitHub projects above
