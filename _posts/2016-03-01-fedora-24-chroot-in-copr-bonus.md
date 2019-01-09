---
id: 237
title: Fedora 24 chroots in Copr + bonus
date: 2016-03-01T16:18:28+00:00
author: adam
guid: http://blog.samalik.com/?p=237
permalink: /fedora-24-chroot-in-copr-bonus/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6211358903"
categories:
  - Copr Build Service
  - Fedora
---
Yesterday, [Miroslav](https://badges.fedoraproject.org/user/msuchy) added _fedora-24-i386_ and _fedora-24-x86_64_ chroots to [Copr.](https://copr.fedoraproject.org) Chroot for powerPC will be added soon and will be announced on the copr-devel mailing list.

And what is the bonus? We have added the _fedora-24-*_ chroots to every project which had _fedora-rawhide-*_ enabled, and we have copied the repositories as well. In another words, all projects with fedora rawhide should support fedora 24 automatically. You can thank to [Jakub](https://badges.fedoraproject.org/user/frostyx), who wrote the script, for that.
