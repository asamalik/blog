---
id: 381
title: 'Modular F27 Server Edition &#8211; initial design'
date: 2017-06-22T15:41:57+00:00
author: adam
guid: http://blog.samalik.com/?p=381
permalink: /modular-f27-server-edition-initial-design/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6181886636"
categories:
  - Fedora
  - Modularity
---
Recently, I have started a <a href="https://lists.fedoraproject.org/archives/list/server@lists.fedoraproject.org/thread/O4LXIRPAF7GQYRPXPWTHTLIC6FMTZTLX/" target="_blank">discussion on the Server mailing list</a> about building the Fedora 27 Server Edition using <a href="https://docs.pagure.org/modularity/" target="_blank">Modularity</a>. Langdon White is already working on a <a href="https://fedoraproject.org/wiki/Changes/Modular_Server" target="_blank">change request</a>. If that happens, there will be a lot of work in front of us. So let&#8217;s start with writing blog posts!

<span style="font-weight: 400;">To build the Fedora 27 Server Edition using Modularity, Adam thinks we need to focus on </span>**two things**<span style="font-weight: 400;">:</span>

**First** <span style="font-weight: 400;">is the </span>**initial design** <span style="font-weight: 400;">of the basic set of modules for the F27 Server Edition &#8211; including the Host and Platform modules, as well as other &#8216;application/content&#8217; modules. To make this easier, I&#8217;m proposing a tool temporarily called The Graph Thing.</span>

**Second** <span style="font-weight: 400;">is a </span>**great packager UX** <span style="font-weight: 400;">for the build pipeline. This will lead to more content built by the community. It will include The Graph Thing and </span>[<span style="font-weight: 400;">BPO</span>](https://github.com/fedora-modularity/BPO)<span style="font-weight: 400;">, and I will be talking about it in a different post.</span>

**This post covers the first part** <span style="font-weight: 400;">&#8211; the initial design.</span>

# <span style="font-weight: 400;">Modularizing the F27 Server Edition &#8211; introduction</span>

<span style="font-weight: 400;">To build Fedora 27 Server Edition using Modularity, we need to split the monolithic distro into smaller modules. Modules can come in multiple streams and on independent lifecycles. However, in Fedora 27, all modules will be on the same lifecycle of 13 months as the rest of Fedora 27.</span>

[<img class="aligncenter size-large wp-image-382" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/F27-server-edition-split-1024x489.png" alt="Splitting Fedora 27 into modules" width="600" height="287" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/F27-server-edition-split.png)

<span style="font-weight: 400;">The Platform team defines the </span>**Host** <span style="font-weight: 400;">and </span>**Platform** <span style="font-weight: 400;">modules by deciding which packages are needed in which modules and including their dependencies into these modules. They already started defining the Host and Platform modules in the </span>[<span style="font-weight: 400;">Host and Platform GitHub repository</span>](https://github.com/fedora-modularity/hp)<span style="font-weight: 400;">.</span>

**Other modules** <span style="font-weight: 400;">will be defined based on the Fedora 27 Server Edition use-cases. We need to create modules for all server roles and other components that will be part of the server. Defining these modules will also influence the </span>**Platform** <span style="font-weight: 400;">module as it will include some of the packages shared between other modules.</span>

**Splitting the distribution** <span style="font-weight: 400;">into individual modules </span>**is not easy**<span style="font-weight: 400;">. We need to work with hundreds of packages with complex dependencies and carefully decide what package goes into which module. To do the initial distribution design, I am proposing a tool that will help us. I temporarily call it </span>**The Graph Thing** <span style="font-weight: 400;">and I hope the name will change soon.</span>

**After the initial split**<span style="font-weight: 400;">, we expect other </span>**people adding modules** <span style="font-weight: 400;">to the distribution as well. Making the </span>**packager UX great** <span style="font-weight: 400;">is crucial for us, if we want to get a lot of content from the community. Packagers will be also able to use The Graph Thing for the initial design of their module, and </span>**Build Pipeline Overview (BPO)** <span style="font-weight: 400;">to monitor their builds.</span>

# <span style="font-weight: 400;">The Graph Thing &#8211; a tool for the initial design</span>

<span style="font-weight: 400;">The Graph Thing is a tool that will </span>**help people** <span style="font-weight: 400;">with the</span> **initial design** <span style="font-weight: 400;">of individual modules</span> <span style="font-weight: 400;">when</span> **modularizing a distribution**<span style="font-weight: 400;">. It will also help packagers with adding other modules later on.</span>

<span style="font-weight: 400;">It will work with </span>**resources** <span style="font-weight: 400;">from the Fedora infrastructure, </span>**inputs** <span style="font-weight: 400;">from the user, and will produce a </span>**dependency graph** <span style="font-weight: 400;">as an output. An example with pictures is better than a thousand words:</span>

## <span style="font-weight: 400;">Example &#8211; defining a nodejs module</span>

[<img class="aligncenter size-large wp-image-383" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/the-dependency-thing-1024x364.png" alt="The Dependency Thing - first run" width="600" height="213" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/the-dependency-thing.png)

<span style="font-weight: 400;">In this example, there are three things available as </span>**resources**<span style="font-weight: 400;">:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Host module definition</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Platform module definition</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Fedora 27 repository &#8211; including all the Fedora 27 packages</span>
</li>

<span style="font-weight: 400;">A </span>**packager** <span style="font-weight: 400;">wants to add a new module: nodejs. The packager have specified in the </span>**input** <span style="font-weight: 400;">that they want to visualize the </span>_<span style="font-weight: 400;">host</span>_ <span style="font-weight: 400;">and </span>_<span style="font-weight: 400;">platform</span>_ <span style="font-weight: 400;">modules, as well as the new </span>_<span style="font-weight: 400;">nodejs</span>_ <span style="font-weight: 400;">module which doesn&#8217;t exist in the infrastructure. The packager added a </span>_<span style="font-weight: 400;">nodejs-6.1</span>_ <span style="font-weight: 400;">package into that module and wants to see if that&#8217;s enough for the module, or if they need to add something else.</span>

<span style="font-weight: 400;">The </span>**output** <span style="font-weight: 400;">shows that the </span>_<span style="font-weight: 400;">nodejs</span>_ <span style="font-weight: 400;">module will require two other packages directly, </span>_<span style="font-weight: 400;">library-foo-3.6</span>_ <span style="font-weight: 400;">and </span>_<span style="font-weight: 400;">nodejs-doc-6.1</span>_<span style="font-weight: 400;">, and that the </span>_<span style="font-weight: 400;">nodejs-doc-6.1</span>_ <span style="font-weight: 400;">also needs a </span>_<span style="font-weight: 400;">crazy-thing-1.2</span>_<span style="font-weight: 400;">. </span>

<span style="font-weight: 400;">Seeing this, the </span>**packager** <span style="font-weight: 400;">made the following decision:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">The </span><i><span style="font-weight: 400;">library-foo-3.6</span></i><span style="font-weight: 400;"> is a package specific for </span><i><span style="font-weight: 400;">nodejs</span></i><span style="font-weight: 400;">, so it should be part of the </span><i><span style="font-weight: 400;">nodejs</span></i><span style="font-weight: 400;"> module.</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">The </span><i><span style="font-weight: 400;">nodejs</span></i><span style="font-weight: 400;"> module should not include documentation, as it will be shipped separately. They will modify the </span><i><span style="font-weight: 400;">nodejs-6.1</span></i><span style="font-weight: 400;"> package not to include the </span><i><span style="font-weight: 400;">nodejs-doc-6.1</span></i><span style="font-weight: 400;">.</span>
</li>

<span style="font-weight: 400;">With the decision done, the </span>**packager wants to see how it&#8217;s going to look like** <span style="font-weight: 400;">if they apply the changes. So they modify the input of The Graph Thing and run it again:</span>

[<img class="aligncenter wp-image-389 size-large" src="https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/the-dependency-thing21-1024x364.png" alt="" width="600" height="213" />](https://blog-shaman.rhcloud.com/wp-content/uploads/2017/06/the-dependency-thing21.png)

<span style="font-weight: 400;">Great! It looks like that the module now includes everything that is needed. The packager can make the change in the </span>_<span style="font-weight: 400;">nodejs-6.1</span>_ <span style="font-weight: 400;">package and submit this module for a build in the Fedora infrastructure.</span>

## <span style="font-weight: 400;">Value of The Graph Thing tool</span>

<span style="font-weight: 400;">As we saw in the example above, the tool can </span>**help with designing new modules** <span style="font-weight: 400;">by looking at the Fedora 27 packages and giving an instant view of how a certain change could look like, without rebuilding stuff.</span>

<span style="font-weight: 400;">It will also help us identify which </span>**packages** <span style="font-weight: 400;">need to be </span>**shared** <span style="font-weight: 400;">between individual modules, so we can decide if we include them in the Platform, or it we make a shared module. An obvious example of a shared module can be a language runtime, like Python or Perl. Other, not that obvious, can be identified with this tool.</span>

<span style="font-weight: 400;">Apart from the initial design of the Fedora 27 Server Edition, this tool could be also a part of the </span>**packager UX** <span style="font-weight: 400;">which I will be talking about soon.</span>

## <span style="font-weight: 400;">Early implementation</span>

<span style="font-weight: 400;">I have already created an early partial implementation of this tool. You can find it in my </span>[<span style="font-weight: 400;">asamalik/modularity-dep-viz GitHub repo</span>](https://github.com/asamalik/modularity-dep-viz)<span style="font-weight: 400;">.</span>

## <span style="font-weight: 400;">Next steps</span>

<span style="font-weight: 400;">The tool needs to get rewritten to use </span>**libsolv** <span style="font-weight: 400;">instead of multiple repoquery queries &#8211; so it produces the correct output, and takes seconds rather than minutes to produce an output. It could also be merged with another similar project called </span>[<span style="font-weight: 400;">depchase</span>](https://github.com/fedora-modularity/depchase) <span style="font-weight: 400;">which has been used by the Platform team to define the Base Runtime and Bootstrap modules for the F26 Boltron release.</span>
