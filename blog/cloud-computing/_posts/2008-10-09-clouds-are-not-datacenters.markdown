---
author: Randy Bias
comments: true
date: 2008-10-09 02:15:41+00:00
layout: post
slug: clouds-are-not-datacenters
title: Clouds are not Datacenters
wordpress_id: 2362
old_categories:
- Cloud Computing
- Technology
---

There is ongoing confusion about the relationship between clouds and datacenters.  You can see this with the term 'virtual datacenter' in reference to servers in the cloud or the lengths to which some folks go to bring datacenter-centric methodologies to the cloud[1].  Unfortunately, clouds are not datacenters.  They ride on top of datacenters, they span datacenters, but they are **not** a datacenter.

Why does this matter, what's the difference, and how are they related?

Read on for more.<!-- more -->

**What is a Datacenter?**
Once again, Wikipedia to the rescue where we find that a [datacenter](http://en.wikipedia.org/wiki/Data_center) is:

>... a facility used to house computer systems and associated components, such as telecommunications and storage systems. It generally includes redundant or backup power supplies, redundant data communications connections, environmental controls (e.g., air conditioning, fire suppression) and security devices.

This is a nice clean definition, but what should immediately jump out at you is how tied to locality the notion of a datacenter is.  It has specific redundant power supplies, redundant communications, environmental controls, and it's own security devices.

A datacenter is a specific place housing specific servers.  Clearly clouds need a datacenter, but the actual promise of clouds is that you no longer need to think about datacenters.

Where are you servers? [2]

>_Out there.  Somewhere. In the clouds. You don't know. You don't care._

**Clouds**
Being an abstraction of datacenters, clouds are a representation of the very notion of location independence.  The 'cloud' will give you some resources: storage, servers, applications, and you don't care where or how so long as they are reasonably reliable and redundant.

Reliability and redundancy comes from cloud providers using multiple datacenters, so clouds almost certainly span one or more datacenters, but themselves are not datacenters.

The canonical example of this is Amazon Web Services (AWS), the market leader.  They have three distinct 'availability zones', which they guarantee to be 100% independent in terms of power, cooling, network, storage, etc.  However, your cloud interface is a single interface to all three 'zones'.

At the very least, the market demands this.  We work with a number of different cloud providers and all are either already multi-site, multi-datacenter in nature, or planning to be in the near future.

A brief aside:  it's worth pointing out that while clouds don't care about a particular locality, they care deeply about relative network locality and topography.  For example, if you want to serve Europe, you would rather do it from a European cloud, or even U.S. west coast users from the location 'closest' to them.  You still aren't particular **where** the datacenters that support that cloud are.  Just that they are 'close' to the market you serve.  I talked very briefly about the 'reach' of clouds in an earlier posting [here](http://neotactics.com/blog/technology/cloud-values/).

**The Cloud Abstraction**
So, tying this down a bit further, you can think of clouds as an abstraction of the raw parts that a datacenter provides:  servers, storage, networking, etc.

Datacenters give you specific servers, network, storage, power and cooling.  Clouds provide you abstracted versions of these components that are not tied to a specific datacenter: virtual servers, virtual storage, and virtual networking.

Why do we need an abstraction?  Because it allows us to think about and use infrastructure in a new (old) way that is fundamental to how the Internet functions.  This notion is called 'distributed computing'.

**Distributed Computing**
The distributed computing entry on Wikipedia gives us some background, but suffers from an academic writing style.  A simpler definition is:

A programming paradigm focusing on designing distributed, open, scalable, transparent, fault tolerant systems. This paradigm is a natural result of the use of computers to form networks.

Distributed computing techniques are the result of our highly connected computers.  Cloud computing is simply a natural outgrowth of the need to service our desire to build distributed, open, scalable, transparent, and fault tolerant applications.  What is Google if not one gigantic distributed computing application?

Datacenters come from an older mainframe paradigm.  Clouds are a result of the need for a new paradigm that is highly distributed and highly connected.

**Clouds as Distributed Computing**
Clouds are a form of distributed computing.  Distributed computing can be simplified down to the act of running software or an application in a multi-server, distributed manner.  While you can run an application distributed within a single datacenter, usually this is not considered 'distributed'.

There is a classic set of concerns about distributed computing that are very well formed called the [Fallacies of Distributed Computing](http://en.wikipedia.org/wiki/Fallacies_of_Distributed_Computing).  Briefly recapped, the Fallacies are:

  1. The network is reliable.
  2. Latency is zero.
  3. Bandwidth is infinite.
  4. The network is secure.
  5. Topology doesn't change.
  6. There is one administrator.
  7. Transport cost is zero.
  8. The network is homogeneous.

These fallacies explain the traditional problems with distributed computing, but although you might have a multi-server application in your local datacenter, the datacenter environments themselves mask most of the normal distributed computing issues.  This is because inside a single location, the network is usually very reliable, extremely low latency, high bandwidth, secure, stable, under a single user or group's control, and homogeneous, or nearly so.

Clouds (re)surface all of these distributed computing concerns that are so critical.  What do you do when the network or systems are unreliable?  When latency is highly variable?  When a potential attacker can be on the wire between any two nodes?

These are critical questions that matter when considering clouds vs. datacenters.

**Why Does the Distinction Matter?**
It matters because the older datacenter-centric model of systems management is more of a centralized and monolithic model that does not take into account the Fallacies of Distributed Computing nor the ephemeral nature of the clouds themselves.  Today's datacenter tools and methodologies are focused either on the datacenter itself or on individual servers.  For example, you'll find many enterprise 'datacenter management' tools today, but none are suitable to managing clouds.  You'll also find a bevy of tools that help you manage a single server or even a small group of servers, but you need more than this in the cloud.

Just digging in briefly, if you look at a typical datacenter there is significant support infrastructure that facilitates the efficient running of that datacenter, like:

  * NTP (Network Time Protocol) servers for synchronizing time
  * DNS (Domain Name Service) servers for mapping hostnames to IP addresses
  * DHCP servers to give hosts IP addresses
  * Network installation systems such as Kickstart, Jumpstart, and RIS
  * Monitoring services such as Nagios, Munin, HP OpenView, and Sitescope
  * Power control and environmental metrics are also necessary

This isn't even a complete list and many of these tools are either unnecessary or unfeasible in the cloud yet most of the functionality is still required. The functionality is usually delivered in a different manner than inside the datacenter.  Most datacenter management tools don't map directly to the cloud.  New solutions are needed or the old tools need to be changed.

So if the cloud isn't a datacenter, if those tools don't map, if managing a single server isn't enough, and if you want to be able to scale your application, then what makes sense?

**Cloud Oriented Architectures**
Cloud Oriented Architecture (COA) is an application-centric architecture.  What does it mean to be application-centric?  I think we're still figuring this out, but at the very least, being application centric means:

  * Deploy your application wherever you like: external clouds or internal datacenters
  * Applications can go on one server or many
  * Add more resources and capacity to your application at any time
  * Composite your application from many 'services'; on one cloud or many
  * Determine the health and state of your application on demand

For additional ideas, James Urquhart (The Wisdom of Clouds) takes a [deep dive](http://blog.jamesurquhart.com/2008/08/principles-of-cloud-oriented.html) into COA.

One thing you might have started to notice is that COA is similar to other well established distributed computing application architectures like [Service Oriented Architecture](http://en.wikipedia.org/wiki/Service-oriented_architecture) (SOA), [Event Driven Architecture](http://en.wikipedia.org/wiki/Event-driven_architecture) (EDA), and related.  These are **developer** notions more than they have been operations, IT, and systems administrator notions historically.

**Operations in the Cloud**
Cloud Oriented Architectures, cloud APIs, and the difference between clouds and datacenter paradigms mean that there are many new challenges for IT and Operations folks.  Most of the early adopters and innovators in the cloud to date have been developers, like Don McAskill of SmugMug and his exploits with [SkyNet](http://blogs.smugmug.com/don/2008/06/03/skynet-lives-aka-ec2-smugmug/).  There is still a dearth of operations and IT experts developing innovative new tools in the cloud.  This is part of the neoTactics focus and the reason for the [CloudScale Project](http://neotactics.com/cloudscale/).

It's going to take new and ongoing innovation to deliver COA to the cloud melding the skills of developers and wisdom of Internet, IT, and web operators.

* * *

[1] http://www.itbusinessedge.com/blogs/dcc/?p=72
[2] Please excuse my attempt at Haiku.  :)
