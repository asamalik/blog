---
id: 223
title: Make your Gnome title bars smaller
date: 2016-02-03T10:18:02+00:00
author: adam
guid: http://blog.samalik.com/?p=223
permalink: /make-your-gnome-title-bars-smaller/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6181894662"
categories:
  - Fedora
---
**Update: See the [updated version for Gnome 3.20 and Fedora 24.](http://blog.samalik.com/make-your-gnome-title-bar-smaller-fedora-24-update/)**

I don&#8217;t like the size of title bars in the stock Gnome 3. They are big and take to much space on my tiny 12&#8243; screen! But I&#8217;ve found an easy solution to this.

[<img class="aligncenter size-full wp-image-225" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2016/02/gnome-window-title-bar.png" alt="gnome-window-title-bar" width="838" height="320" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2016/02/gnome-window-title-bar.png)All you need to do is to put the following css code into ~/.config/gtk-3.0/gtk.css

<pre>.header-bar.default-decoration {
 padding-top: 3px;
 padding-bottom: 3px;
 font-size: 0.8em;
}

.header-bar.default-decoration .button.titlebutton {
 padding: 0px;
}</pre>
