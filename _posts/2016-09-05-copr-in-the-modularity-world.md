---
id: 294
title: Copr in the Modularity World
date: 2016-09-05T16:55:28+00:00
author: adam
guid: http://blog.samalik.com/?p=294
permalink: /copr-in-the-modularity-world/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6211778270"
categories:
  - Copr Build Service
  - Fedora
  - Modularity
---
<span style="font-weight: 400;"><a href="https://copr.fedorainfracloud.org" target="_blank">Copr</a> is a community build service in Fedora that enables anyone with a FAS account to build their own RPM repositories. This post explains how we can use Copr in modularity, what is already supported, and what needs to be done.</span>

<span style="font-weight: 400;">Almost everything in this post starts with a view from the UX perspective. However, technical details are also provided as they are the crucial part of this post.</span>

I have also created a <a href="https://www.youtube.com/watch?v=uNW8QEzsdDg" target="_blank"><strong>YouTube video</strong> showing building modules in Copr + installing</a>.

## What I want to achieve

### Build systems in Fedora

<span style="font-weight: 400;">There are two build systems in Fedora currently: </span>

  1. **Koji** <span style="font-weight: 400;">is the official Fedora build service, that builds everything officially released in Fedora.</span>
<li style="font-weight: 400;">
  <b>Copr</b><span style="font-weight: 400;"> is a community build service, available to anyone to build their own RPM repositories. Packages here are not reviewed. Copr in Fedora is something like AUR in Arch Linux.</span>
</li>

<span style="font-weight: 400;">The purpose of these two build systems should remain unchanged in the modular world. Fedora modules would be built in Koji, and community modules would be built in Copr.</span>

### Producing modules

<span style="font-weight: 400;">A simplified examples of workflows to build modules in both build systems could be as follows:</span>

  * ****Koji**<span style="font-weight: 400;">:</span>** 
      1. **By submitting a modulemd yaml**<span style="font-weight: 400;">. The whole module including its packages will be built automatically in the pipeline.</span>
  * ****Copr**<span style="font-weight: 400;">:</span>** 
      1. **By** **submitting a modulemd yaml**<span style="font-weight: 400;">. The whole module including its packages will be built automatically in the pipeline.</span>
      2. **By “handcrafting” the module manually**<span style="font-weight: 400;">. User would submit the builds one by one &#8211; as they would in Copr today &#8211; and then build a module out of the project. This workflow is described in a more detail below.</span>

**Copr** <span style="font-weight: 400;">could be used </span>**to build the initial versions of modules** <span style="font-weight: 400;">that would eventually end up </span>**in** **Fedora**<span style="font-weight: 400;">. The “Handcrafting” feature will allow packagers to build and develop their module gradually, and submit it for review in Fedora later when it is ready.</span>

### Consuming modules

**Official/production modules** <span style="font-weight: 400;">in Fedora would be identified by </span>**‘name-branch-version’**<span style="font-weight: 400;">. To install a LAMP stack from Fedora, user would do something like:</span>

<pre><span style="font-weight: 400;">$ module-thing install LAMP-something-42
</span></pre>

**Community modules from Copr** <span style="font-weight: 400;">would be identified by </span>**‘username/name-branch-version’**<span style="font-weight: 400;">. To install a LAMP stack from Copr created by user asamalik, user would do something like:</span>

<pre><span style="font-weight: 400;">$ module-thing install asamalik/LAMP-something-42</span></pre>

<span style="font-weight: 400;">Important detail in both scenarios is </span>**using** <span style="font-weight: 400;">of </span>**the same tools** <span style="font-weight: 400;">to consume both official and community versions.</span>

## Technical &#8211; modules in Koji vs. modules in Copr

<span style="font-weight: 400;">This table is a summary of the main differences. It is also described in a bit more detail below.</span>

<table>
  <tr>
    <td>
    </td>
    
    <td>
      <b>Koji</b>
    </td>
    
    <td>
      <b>Copr</b>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">Modules are represented by</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Tags</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Projects</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">Build roots are defined by</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">RPMs with a specific tag</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">External RPM repositories</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">Finished module builds are</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">RPMs with a specific tag</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">RPM repository</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">Multiple packages with the same NVR + dist-tag in the build system</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">No</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Yes &#8211; every project has its own isolated namespace for packages.</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">Multiple modules with the same name in the build system</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">No</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Yes &#8211; every user has its own isolated namespace for modules.</span>
    </td>
  </tr>
</table>

### Koji

<span style="font-weight: 400;">Koji uses </span>**tags** <span style="font-weight: 400;">to work with modules, where tag is basically a group of RPM packages. Each module has a ‘build tag’ with all RPMs defining the build root, and a ‘module tag’ with all the built RPMs that are included in the module as components. </span>

<span style="font-weight: 400;">A single RPM can be tagged with multiple tags. The </span>**problem** <span style="font-weight: 400;">is, that there can not be multiple RPMs in Koji with the same NVR and dist-tag. To workaround this problem, we modify the dist-tag of all RPMs in a module to include the name of the module.</span>

<span style="font-weight: 400;">Koji can/will be able to create an RPM repository out of every ‘module tag’ using a ‘signed repo’ function.</span>

### Copr

<span style="font-weight: 400;">Copr would use </span>**projects** <span style="font-weight: 400;">to work with modules, where project is something like a directory. One project can define a build root by selecting a predefined mock chroot. This build root can be modified by linking external RPM repositories. To build modules, Copr would introduce an empty mock chroot, and the build root could be defined only by the RPM repository.</span>

<span style="font-weight: 400;">A single RPM can be included in only one project. To include one RPM in more projects, it needs to be rebuilt in them. However, there can be multiple packages with the same NVR and dist-tag in Copr. One in every project.</span>

Copr also supports namespaces which is done by usernames. For example, two users can create modules with the same name, stream, release, metadata, … and include an RPM package with the same NVR + dist-tag. These will be completely separated.

<span style="font-weight: 400;">Copr automatically creates a signed RPM repository out of every project. “Modularization” of the repository with a yaml spec file is already supported.</span>

## Building modules in Copr &#8211; conceptual view

<span style="font-weight: 400;">This section describes steps that needs to be performed in Copr to build a module. </span>**The following steps can be done by a user or an automated tool like the orchestrator.**

<span style="font-weight: 400;">Copr currently supports everything except empty chroots and releasing a module.</span>

### Building a module

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Create a project with empty chroot</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Define build root by linking external repository</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Build all your RPM packages</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Release a module, two ways doing that:</span> <ol>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Define the module API, install profiles, and package filters by selecting binary packages from a list. [supported soon]</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Add the modulemd yaml to the repository. [already supported]</span>
    </li>
  </ol>
</li>

### Building a stack

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Create a project with empty chroot &#8211; let’s call it the </span><i><span style="font-weight: 400;">main project</span></i>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Create projects for all the “submodules” in your stack &#8211; let’s call them </span><i><span style="font-weight: 400;">submodule projects</span></i>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Define build root by linking external repository to all projects you have created</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Build all your RPM packages of your “submodules” in their projects</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Use the “fork” function in Copr to copy the built RPMs from all your submodule project to the main project</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Delete all the submodule projects</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Release a module, two ways doing that:</span> <ol>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Define the module API, install profiles, and package filters by selecting binary packages from a list. [supported soon]</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Add the modulemd yaml to the repository. [already supported]</span>
    </li>
  </ol>
</li>

### Handcrafting projects in Copr

<span style="font-weight: 400;">This method of building modules is meant for the community members that use Copr today. The </span>**main benefits** <span style="font-weight: 400;">are:</span>

<li style="font-weight: 400;">
  <b>Users will not need to write the yaml spec</b><span style="font-weight: 400;"> &#8211; Copr will automatically generate it for them.</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">User&#8217;s workflow of creating a module will be very similar to how they create RPM repositories in Copr today.</span>
</li>

<span style="font-weight: 400;">However, Copr will also support rebuilding modules from Fedora or building custom modules by submitting the yaml spec.</span>

#### Workflow

<li style="font-weight: 400;">
  <span style="font-weight: 400;">User creates a project</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">User defines build root by selecting a “base runtime module” from Fedora &#8211; roughly the same way as they would select chroots today</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">User builds all their RPM packages</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">User defines the module API, install profiles, and package filters by clicking checkboxes (see mockup below)</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">User then click on “release module”. Copr will generate the yaml spec for them automatically and create a modular RPM repository.</span>
</li>

<span style="font-weight: 400;">The picture below shows the UI in Copr to create a module out of a project.</span>

### Producing traditional repo and module at the same time

<span style="font-weight: 400;">Copr supports multiple chroots in one project. That means I can build the same thing for example for Fedora 23, Fedora 24, Epel 6, and Epel 7. We could add “module” as another chroot, so user could build the same thing for old and new systems. Traditional repositories could be consumed anytime &#8211; including installation and updates. Modules would be released every time project enters a release milestone. Modules would remain unchanged forever &#8211; the same way as in Fedora.</span>
