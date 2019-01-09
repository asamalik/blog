---
id: 316
title: Early module development with Fedora Modularity
date: 2017-01-19T12:01:07+00:00
author: adam
guid: http://blog.samalik.com/?p=316
permalink: /early-module-development-with-fedora-modularity/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6185598646"
categories:
  - Fedora
  - Modularity
---
So you like the <a href="https://fedoraproject.org/wiki/Modularity" target="_blank">Fedora Modularity project</a> &#8211; where we <a href="https://www.youtube.com/watch?v=xNLhcYEMgO0" target="_blank">separate the lifecycle of software from the distribution</a> &#8211; and you want to start with module development early? Maybe to have it ready for the <a href="https://fedoraproject.org/wiki/Changes/Modular_Server_Preview" target="_blank">modular Fedora 26 Server preview</a>? Start developing your <a href="https://pagure.io/modulemd" target="_blank">modulemd</a> on your local system now, and have it ready for later when the <a href="https://fedoraproject.org/wiki/Changes/ModuleBuildService" target="_blank">Module Build Service is in production</a>!

## Defining your module

To have your module build, you need to start with writing a <a href="https://pagure.io/modulemd" target="_blank">modulemd</a> file which is a definition of your module including the components, API, and all the information necessary to build your module like specifying the build root and a build order for the packages. Let&#8217;s have a look at an example Vim module:

<pre>document: modulemd
version: 1
data:
    summary: A ubiquitous text editor
    description: &gt;
        Vim is a highly configurable text editor built to make creating and
        changing any kind of text very efficient.
    license:
        module:
            - MIT
        content: []
    xmd: ~
    dependencies:
        buildrequires:
            generational-core: master
        requires:
            generational-core: master
    references:
        community: http://www.vim.org/
        documentation: http://www.vim.org/docs.php
        tracker: https://github.com/vim/vim/issues
    profiles:
        default:
            rpms:
                - vim-enhanced
        minimal:
            rpms:
                - vim-minimal
        graphical:
            rpms:
                - vim-X11
    api:
        rpms:
            - vim-minimal
            - vim-enhanced
            - vim-X11
    filter:
        rpms: ~
    components:
        rpms:
            vim-minimal:
                rationale: The minimal variant of VIM, /usr/bin/vi.
            vim-enhanced:
                rationale: The enhanced variant of VIM.
            vim-X11:
                rationale: The GUI variant of VIM.
            vim-common:
                rationale: Common files needed by all VIM variants.
            vim-filesystem:
                rationale: The directory structure used by VIM packages.</pre>

Notice that there is no information about the name or version of the module. That&#8217;s because the build system takes this information from the git repository, from which the module is build:

  * Git repository name == module name
  * Git repository branch == module stream
  * Commit timestamp == module version

You can also see my own <a href="https://github.com/asamalik/proftpd" target="_blank">FTP module</a> for reference.

To build your own module, you need to create a Git repository with the modulemd file. The name of your repo and the file must match the name of your module:

<pre>$ mkdir my-module
$ touch my-module/my-module.yml</pre>

The core idea about modules is that they include all the dependencies in themselves. Well, except the base packages found in the Base Runtime API &#8211; which haven&#8217;t been defined yet. But don&#8217;t worry, you can use this <a href="https://github.com/contyk/base-runtime/blob/master/api.txt" target="_blank">list of binary packages</a> in the meantime.

So the _components_ list in your modulemd need to include all the dependencies except the ones mentioned above. You can get a list of recursive dependencies for any package by using _repoquery_:

<pre>$ repoquery --requires --recursive --resolve PACKAGE_NAME</pre>

When you have this ready, you can start with building your module.

## Building your module

To build a modulemd, you need to have the <a href="https://pagure.io/fm-orchestrator" target="_blank">Module Build Service</a> installed on your system. There are two ways of achieving that:

  1. Installing the <a href="https://bugzilla.redhat.com/show_bug.cgi?id=1404012" target="_blank">module-build-service package</a> with all its dependencies.
  2. Using a <a href="https://github.com/asamalik/build-module" target="_blank">pre-built docker image and a helper script</a>.

Both options provide the same result, so choose whichever you like better.

### Option 1: module-build-service package

On **Fedora rawhide**, just install it by:

<pre>$ sudo dnf install module-build-service</pre>

I have also created a <a href="https://copr.fedorainfracloud.org/coprs/asamalik/mbs/" target="_blank">Module Build Service copr repo</a> for **Fedora 24** and **Fedora 25**:

<pre>$ sudo dnf copr enable asamalik/mbs
$ sudo dnf install module-build-service</pre>

To build your modulemd, run a command similar to the following:

<pre>$ mbs-manager build_module_locally <span class="pl-s">file:////path/to/my-module?#master</span></pre>

An output will be a yum/dnf repository in the /tmp directory.

### Option 2: docker image and a helper script

With this option you don&#8217;t need to install all the dependencies on your system, but it requires you to _setenforce 0_ before the build. 🙁

You only need to clone the <a href="https://github.com/asamalik/build-module" target="_blank">asamalik/build-module repository on GitHub</a> and use the helper script as follows:

    $ build_module ./my-module ./results
    

An output will be a yum/dnf repository in the patch you have specified.

## What&#8217;s next?

The next step would be installing your module on the Base Runtime and testing if it works. But as we are doing this pretty early, there is no Base Runtime at the moment I&#8217;m writing this. However, you can try your module in a container using a pre-build <a href="https://github.com/asamalik/fake-base-runtime-module-image" target="_blank">fake Base Runtime</a> image.

To handcraft your modular container, please follow the <a href="https://fedoraproject.org/wiki/Modularity/Development/Developing_and_Building_Modules" target="_blank">Developing and Building Modules guide</a> on our wiki which provides you all the necessary steps while showing you a way how modular containers might be built in the future infrastructure!

### DevConf.cz 2017

Are you visiting <a href="https://devconf.cz/" target="_blank">DevConf.cz</a> in Brno? There is a talk about Modularity and a workshop where you can try building your own module as well. Both can be found in the <a href="https://devconf.cz/schedule.html" target="_blank">DevConf.cz 2017 Schedule</a>.

  * Day 1 (Friday) at 12:30 &#8211; **Fedora Modularity &#8211; How does it work?**
  * Day 2 (Saturday) at 16:00 &#8211; **Fedora Modularity &#8211; Build your own module!**

See you there!

&nbsp;
