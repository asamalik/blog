---
id: 285
title: 'Roles of PDC and BPO in Modularity &#8211; please give me feedback'
date: 2016-08-16T14:28:08+00:00
author: adam
guid: http://blog.samalik.com/?p=285
permalink: /roles-of-pdc-and-bpo-in-modularity/
catchflames-sidebarlayout:
  - default
dsq_thread_id:
  - "6224764397"
categories:
  - Fedora
  - Modularity
---
<span style="font-weight: 400;">There has been some confusion about the roles of PDC and BPO in Modularity as the roles might seem overlapping. This document will briefly explain the roles of both services and highlight the main differences.</span>

<span style="font-weight: 400;">Long story short:</span>

<li style="font-weight: 400;">
  <b>PDC</b><span style="font-weight: 400;"> is a </span><i><span style="font-weight: 400;">database</span></i><span style="font-weight: 400;"> that stores module metadata and dependency graphs</span>
</li>
<li style="font-weight: 400;">
  <b>BPO</b><span style="font-weight: 400;"> is a </span><i><span style="font-weight: 400;">web UI</span></i><span style="font-weight: 400;"> to display module build state and probably to browse some metadata</span>
</li>

<span style="font-weight: 400;">Main overlaps:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">BPO has its own database. However, the database acts as a cache only to make the UI fast. All the data can be lost and recovered from other services such as Orchestrator and PDC.</span>
</li>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">PDC has its own web UI. However, browsing and displaying modules has not been implemented. And even if it was, PDC does not/should not store data such as build state.</span>
</li>

<span style="font-weight: 400;">From my understanding, this design has been already valid on the Modularity Infra wiki page: </span>[<span style="font-weight: 400;">https://fedoraproject.org/wiki/Modularity/Architecture/Infra?rd=Modularity/Infra</span>](https://fedoraproject.org/wiki/Modularity/Architecture/Infra?rd=Modularity/Infra)

# <span style="font-weight: 400;">PDC &#8211; Product Definition Centre</span>

<span style="font-weight: 400;">PDC is the </span>**primary database** **for module metadata** <span style="font-weight: 400;">such as:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Name, stream, release &#8211; or however are these going to be called</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Dependencies and components</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Koji tags</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Maybe information such as SLA?</span>
</li>

<span style="font-weight: 400;">It provides a </span>**REST API** <span style="font-weight: 400;">to access and manipulate this data.</span>

<span style="font-weight: 400;">A part of PDC is also a web UI that will not be used in Modularity.</span>

# <span style="font-weight: 400;">BPO &#8211; Build Pipeline Overview</span>

<span style="font-weight: 400;">BPO is a </span>**single web UI** <span style="font-weight: 400;">that will watch over the whole pipeline. Its primary function is to show the build state of each module. </span>

<span style="font-weight: 400;">Users will be also able to </span>**browse module metadata** <span style="font-weight: 400;">such as:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Dependencies</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Components</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Install profiles</span>
</li>

<span style="font-weight: 400;">BPO uses its </span>**own database as a cache only** <span style="font-weight: 400;">to make the UI faster. The database:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Will be updated by fedmsg and also queries of other services as reactions to some messages.</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Can be deleted and recovered from other services.</span>
</li>
