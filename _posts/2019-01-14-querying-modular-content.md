---
title: Querying modular content
---

Following up after my [recent post about Modularity content discovery]({{ site.baseurl }}{% post_url 2017-09-12-flock-2017-was-awesome %}) with a neat workaround that works now.

The problem was: I need to do `dnf repoquery` across all module streams, but the way it currently works is that it only works with the default or enabled modules.

I had a quick chat with Jaroslav Mracek from the DNF team and he came up with this interesting workaround: marking the modular repositories as "hotfix" repositories will cause DNF to see all the RPMs in it — in all the module streams.

So let's try.

```
$ dnf --setopt=updates-modular.module_hotfixes=true --setopt=fedora-modular.module_hotfixes=true repoquery --whatprovides /usr/bin/npm
Last metadata expiration check: 0:42:52 ago on Mon 14 Jan 2019 01:24:41 PM UTC.
npm-1:5.6.0-1.8.11.4.1.module_2030+42747d40.x86_64
npm-1:6.4.1-1.10.11.0.1.fc29.x86_64
npm-1:6.4.1-1.10.11.0.1.module_2200+adbac02b.x86_64
npm-1:6.4.1-1.10.13.0.1.module_2362+1451e041.x86_64
npm-1:6.4.1-1.10.15.0.1.fc29.x86_64
npm-1:6.4.1-1.11.1.0.1.module_2379+8d497405.x86_64
```

Looks like that works! The list contains packages from all three Node.js streams.

And to find out what module contains each package, I can do:

```
$ dnf --setopt=updates-modular.module_hotfixes=true --setopt=fedora-modular.module_hotfixes=true module provides npm-1:6.4.1-1.11.1.0.1.module_2379+8d497405.x86_64 | grep "^Module"
Module   : nodejs:11:20181102165620:6c81f848:x86_64
Module   : nodejs:11:20181102165620:6c81f848:x86_64
```

Let's put those two together in a single lovely command like this:

```
$ for i in $(dnf --setopt=updates-modular.module_hotfixes=true --setopt=fedora-modular.module_hotfixes=true repoquery --whatprovides /usr/bin/npm); do echo $i; dnf --setopt=updates-modular.module_hotfixes=true --setopt=fedora-modular.module_hotfixes=true module provides $i | grep "^Module" ; echo ""; done
Last metadata expiration check: 0:47:12 ago on Mon 14 Jan 2019 01:24:41 PM UTC.
npm-1:5.6.0-1.8.11.4.1.module_2030+42747d40.x86_64
Module   : nodejs:8:20180816123422:6c81f848:x86_64
Module   : nodejs:8:20180816123422:6c81f848:x86_64
Module   : nodejs:8:20180816123422:6c81f848:x86_64

npm-1:6.4.1-1.10.11.0.1.fc29.x86_64

npm-1:6.4.1-1.10.11.0.1.module_2200+adbac02b.x86_64
Module   : nodejs:10:20180920144631:6c81f848:x86_64

npm-1:6.4.1-1.10.13.0.1.module_2362+1451e041.x86_64
Module   : nodejs:10:20181101171344:6c81f848:x86_64

npm-1:6.4.1-1.10.15.0.1.fc29.x86_64

npm-1:6.4.1-1.11.1.0.1.module_2379+8d497405.x86_64
Module   : nodejs:11:20181102165620:6c81f848:x86_64
Module   : nodejs:11:20181102165620:6c81f848:x86_64
```

Someone could call that usable, right?

I've polished the output a bit and put it in a shell script you can get in [my github repo asamalik/modular-repoquery](https://github.com/asamalik/modular-repoquery):

```
$ ./modular-repoquery --whatprovides /usr/bin/npm
Last metadata expiration check: 1:05:14 ago on Mon 14 Jan 2019 01:24:41 PM UTC.
npm-1:5.6.0-1.8.11.4.1.module_2030+42747d40.x86_64 (nodejs:8:20180816123422:6c81f848:x86_64)
npm-1:6.4.1-1.10.11.0.1.fc29.x86_64 
npm-1:6.4.1-1.10.11.0.1.module_2200+adbac02b.x86_64 (nodejs:10:20180920144631:6c81f848:x86_64)
npm-1:6.4.1-1.10.13.0.1.module_2362+1451e041.x86_64 (nodejs:10:20181101171344:6c81f848:x86_64)
npm-1:6.4.1-1.10.15.0.1.fc29.x86_64 
npm-1:6.4.1-1.11.1.0.1.module_2379+8d497405.x86_64 (nodejs:11:20181102165620:6c81f848:x86_64)
```

It's a bit slow because of the loop, but hey, it does what we need!