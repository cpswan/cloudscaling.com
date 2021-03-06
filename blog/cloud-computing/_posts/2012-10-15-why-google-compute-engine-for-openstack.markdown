---
author: Randy Bias
comments: true
date: 2012-10-15 00:02:18+00:00
layout: post
slug: why-google-compute-engine-for-openstack
title: Why Google Compute Engine for OpenStack
wordpress_id: 5278
old_categories:
- Cloud Computing
---

We [announced](http://www.prweb.com/releases/2012/10/prweb10007992.htm) on Thursday the availability of a new compute API set for [OpenStack](http://www.openstack.org) that is compatible with [Google Compute Engine](https://cloud.google.com/products/compute-engine) (GCE).  GCE is Google's Infrastructure-as-a-Service (IaaS) compute service that competes with Amazon Web Services EC2.  The announcement was picked up by [TechCrunch](http://techcrunch.com/2012/10/12/cloudscaling-opens-google-compute-engine-apis-to-openstack-provides-alternative-to-amazon-web-services/).  _**This makes OpenStack the first IaaS software solution to support the GCE APIs.**_

We hope that the OpenStack community will embrace and accept this code.  Regardless, Cloudscaling will provide support and updates for this API to use with OpenStack.  This blog posts hopes to answer a few common questions we have received.

**How was the code implemented?**
The GCE APIs for OpenStack Compute look almost identical to the two existing compute APIs: EC2 and Nova.  The GCE APIs are implemented as first-class citizens of OpenStack Compute and provide a RESTful API that is highly compatible with Google Compute Engine.

This is an initial BETA of the code that is probably mostly experimental, although most functionality is there and most things have been thoroughly tested.  There will be a blog posting here on Monday the 15th (tomorrow) when the code goes live on the [Cloudscaling Github repository](https://github.com/cloudscaling).  The README will provide additional information about which exact GCE API functionality is supported.

**Why did you do this?**
Our customers are asking for two interrelated items: federation to public clouds and a choice of public cloud APIs.  It's been very consistent.  Customers are all deploying some kind of hybrid solution.  Some times they start in public and want to move some workloads back to private, like Zynga.  Some times they start in private and want to move some workloads back to public.  Regardless, it's clear they want to run mixed mode for the forseeable future: some capacity in private and some in public.  The challenge, then is for them have private clouds that are compatible with public clouds.  OpenStack provides this already with the EC2 (AWS) and Nova (OpenStack) APIs; however, a number of our customers have professed a strong interest in GCE too.

Problem solved.

**Why GCE?**
Taking aside customer demand, I've personally spent time on Google Compute Engine (GCE) now and I can honestly say that it's a game changer.  While it might be flying under the radar now, I expect this to change in the future.  GCE is really the first major public cloud I have seen, other than AWS, that is designed as a true elastic, scale-out Infrastructure-as-a-Service (IaaS) system.  The new Rackspace OpenStack-based cloud is close, but GCE is really ahead in a number of key areas, including their on-demand block storage service (equivalent to AWS Elastic Block Storage).  This isn't readily apparent unless you have used GCE, because they don't make much noise.

I can tell you this with certitude, GCE is *not* a toy and while they might be in private BETA right now, consider this:  GCE has about 10x the functionality and usability that EC2 had while in private BETA in late 2006.  I should know, I was using EC2 at that time. When GCE becomes more public I fully expect it to ramp harder than AWS did in 2007, when EC2 went from private BETA to public BETA, and to quickly become a viable large-scale alternative to EC2.

**OpenStack Rules**
OpenStack is the new de facto standard cloud infrastructure framework, or the new Linux kernel of the cloud world.  A number of smart companies are going to take OpenStack and run with it to solve real customer problems.  The OpenStack Foundation will work towards creating a level playing field where a number of different OpenStack-powered solutions can engage the marketplace.  The best approaches will win, customers will prosper, and problems will be solved.  We think the GCE APIs are important to OpenStack and it's ecosystem, so we announced them before the OpenStack Design Summit this coming week and we look forward to an engaged discussion with other members of the community around supporting GCE and other public cloud APIs.
