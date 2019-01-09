---
id: 275
title: 'Make your Gnome title bar smaller &#8211; Fedora 24 update'
date: 2016-07-22T08:28:42+00:00
author: adam
guid: http://blog.samalik.com/?p=275
permalink: /make-your-gnome-title-bar-smaller-fedora-24-update/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6181828849"
categories:
  - Fedora
---
I wrote similar [post](http://blog.samalik.com/make-your-gnome-title-bars-smaller/) before about making the massive title bar in Gnome smaller. But it doesn&#8217;t work anymore in Fedora 24!

Don&#8217;t worry, I have created an update for you &#8211; so you can enjoy more space on your desktop again!

[<img class="aligncenter size-full wp-image-225" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2016/02/gnome-window-title-bar.png" alt="gnome-window-title-bar" width="838" height="320" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2016/02/gnome-window-title-bar.png)All you need to do is to put the following css code into ~/.config/gtk-3.0/gtk.css

<pre class="p1"><span class="s1">window.ssd headerbar.titlebar {
</span><span class="s1"><span class="Apple-converted-space">    </span>padding-top: 4px;
</span><span class="s1">    padding-bottom: 4px;
</span><span class="s1">    min-height: 0;
</span><span class="s1">}

</span><span class="s1">window.ssd headerbar.titlebar button.titlebutton {
</span><span class="s1">    padding: 0px;
</span><span class="s1"><span class="Apple-converted-space">    </span>min-height: 0;
</span><span class="s1"><span class="Apple-converted-space">    </span>min-width: 0;
</span><span class="s1">}</span></pre>
