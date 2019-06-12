---
title: Counting packages in Fedora with Modularity
---

I wrote an [article about Modularity for the Fedora Magazine](https://fedoramagazine.org/installing-alternative-rpm-versions-in-fedora/) and I used some numbers there: "At the time of writing — out of the 49,464 binary RPM packages in Fedora 30 — 1,119 (2.26%) come from a module." How did I get to those numbers?

The first step was to list all binary packages in Fedora. Since we have Modularity now, using `dnf repoquery` as it's currently implemented wouldn't show me RPM packages in modules that are not enabled or default. So I used my [modular-repoquery script](https://github.com/asamalik/modular-repoquery) I hacked together a few months ago. That gave me a list of all binary packages in the repositories.

What I want to count? I want to cound every package (by package name) just once. That's one for the non-modular repository, and then one for every module stream. So for example, I counted four `postgresql` packages:

```
postgresql
postgresql (postgresql:10)
postgresql (postgresql:11)
postgresql (postgresql:9.6)
```

To get that, I wrote a series of terrible `sed` commands and put them into a [git repository](https://github.com/asamalik/counting-fedora-packages) along with the generated files (it took about an hour to generate them, the modular-repoquery script is not very efficient, but gets the job done.

Then I just counted all the packages (lines in the `all-names-unique.txt` in that repo to get the total number of packages, and then lines containing the `(` characted to get the modular ones.

Not sure how much useful this is, but I figured I share it anyway!
