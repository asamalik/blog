---
title: Thinking about content discovery in Fedora Modularity 
categories:
  - Fedora
excerpt: 
---

I just had a quick chat with Petr Šabata about content discovery and he had a brilliant idea. But let's first clarify what I mean by content discovery.

```
$ dnf repoquery --whatprovides /usr/bin/node
Last metadata expiration check: 0:35:42 ago on Wed 09 Jan 2019 06:55:52 PM UTC.
nodejs-1:10.11.0-1.fc29.i686
nodejs-1:10.11.0-1.fc29.x86_64
nodejs-1:10.15.0-1.fc29.i686
nodejs-1:10.15.0-1.fc29.x86_64
```

This command is basically asking "What packages provide the `/usr/bin/node` binary in Fedora 29?" But there is something missing...

```
$ dnf module list | grep nodejs
nodejs           8              default, development, minimal, ...              
nodejs           10             default, development, minimal, ...              
nodejs           11             default, development, minimal, ...    
```

There are three Node.js versions in Fedora 29. But I can't see them in the repoquery output...

```
$ dnf -y module enable nodejs:11
$ dnf repoquery --whatprovides /usr/bin/node
Last metadata expiration check: 0:40:33 ago on Wed 09 Jan 2019 06:55:52 PM UTC.
nodejs-1:11.1.0-1.module_2379+8d497405.x86_64
```

That's because currently it only works with default or enabled module streams. We need to fix that because people rely on this information.

Packagers use repoquery to determine which packages to rebuild after making an update to something. Or we can use it to find out if there is a certain version of a library containing a CVE. And no one wants to go enable modules one by one just to do a simple query.

But is it simple, really?

Well, not quite. The repositories don't include all the content. Two classes of data are missing.

First, not every module is shipped. There are a few that are useful only as build dependencies. Some of them are used for bootstrapping for example.

And second is module filters. You can filter certain binary packages out of a module build before you ship it. Again, some of the packages are only useful as build dependencies. But there might be other reasons, too.

So repos are likely out of question because they don't contain all the data we need.

Why do I care about packages that are not being shipped? Because build dependencies influence the output of a build. A simple example would be a compiler. You don't need to ship the compiler for an application to work, but a bug in that compiler can produce bugs (even security ones) in the application. So I need to care about those as well.

I thought about several ways of getting that info from other sources, possibly using the fedmod tool in addition to repoquery, but that all seemed a bit complicated and not right. 

And that's where Petr's idea comes in.

Fedora Infra generates a huge tarball with all the SPEC files of all packages in the distro. That's useful for packagers to grep for stuff when making big changes.

So what if we generated repodata for all packages in the distro?

That means we could just use repoquery on this repodata, and that's it. We would, of course, need to enhance repoquery to actually work with modules, but we'd have to do that anyway.

That seems like an elegant solution.

Thinking further about that, I need to clarify what 'all packages in the distribution' means.

For each Fedora release I need to include all the latest versions of every traditionally-built package. I also need the buildroot which is basically the same thing. Yes, I heard there are two additional packages, so we want those, too.

Regarding modules, again, for each Fedora release, I need to have the latest version of all packages in every module stream. (the latest nodejs:10 packages, the latest nodejs:11 packages, etc.) I need to include all the packages, ignoring module filters. (They've been in the buildroot and that's important, remember?)

Additionally, I also need to include all modules that are build-dependencies of the modules I have already included. And this is recursive.

All the data about what packages are in what release are stored in Koji and Bodhi. The script generating the repodata would need to query these services.

The actual packages and modulemd files are in the massive `/mnt/koji`. The script might need to copy these out to run `createrepo_c`. Or can we somehow leverage Koji tags?

This will need a bit of a thought. Likely coming as another post later. :-)

`<half-serious>` Heck, now thinking about it, can we have a database with all of that? With all Fedora releases, packages, modules, package provides, and all their relations? Is that too crazy? `</half-serious>`

