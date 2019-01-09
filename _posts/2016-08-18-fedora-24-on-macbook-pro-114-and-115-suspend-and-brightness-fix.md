---
id: 290
title: 'Fedora 24 on MacBook Pro 11,4 and 11,5 &#8211; suspend and brightness fix'
date: 2016-08-18T12:47:04+00:00
author: adam
guid: http://blog.samalik.com/?p=290
permalink: /fedora-24-on-macbook-pro-114-and-115-suspend-and-brightness-fix/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6181843998"
categories:
  - Fedora
---
I have a great news for those of you with a MacBook Pro 15&#8243; 2015 (MacBook 11,4 and 11,5)!

As you might have noticed, when running Linux on this machine, it can&#8217;t be suspended, shut down, and you can&#8217;t even control brightness of the display. These issues have been reported a while ago, and yes, there are some patches, but they didn&#8217;t make it to the production code.

Suspend and shutdown: https://bugzilla.kernel.org/show_bug.cgi?id=103211#c172
  
Brightness: https://bugzilla.kernel.org/show_bug.cgi?id=105051#c32

So I took those patches, applied them to the kernel in Fedora and built it in my <a href="https://copr.fedorainfracloud.org/coprs/asamalik/MacBook-kernel/" target="_blank">Copr project</a>.

**How to make it running on your machine?** First, <a href="https://getfedora.org/" target="_blank">download and install Fedora 24</a>. Then you just need to enable my Copr project and install the patched kernel:

<pre>$ sudo dnf copr enable asamalik/MacBook-kernel
$ sudo dnf install kernel-4.6.6-300.AdamsMacBookSleepBrightness.fc24</pre>

Reboot your machine with the patched kernel, and that&#8217;s it!

I will try to keep the repo updated, so you will be able to update kernel as usual.
