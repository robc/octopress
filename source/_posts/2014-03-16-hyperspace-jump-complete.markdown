---
layout: post
title: "Hyperspace Jump Complete"
date: 2014-03-16 18:17
comments: true
categories: [Waffle]
---
Not a big post, but just one to test out publishing under the new setup. For most of the last few years, this blog (and it's incarnation before this one) were originally hosted on a small VPS. The idea at the time of setting that up was that as I was doing lots of web stuff, it'd be great to have an environment where I could configure my own environment & run my own applications away from my own computer.

Of course, focus shifts, directions change, and I found myself doing mobile development instead. As a result, the need to maintain the VPS wasn't as high, and well - it became overkill for my purposes. Plus, the evolution of technology has helped with that, bringing easier deployments to other environments, let alone platform-as-a-service models.

Which, as well as tying in with some personal goals to simplify certain things this year - meant it's time to decommission said VPS. The first phase? Relocating this blog, and sites like the one for [Pocket Dogfights](http://www.pocketdogfights.com) over to a simpler environment.

In this case, with all of these sites being relatively static, the best option available was Amazon's S3 - which I wasn't aware could be easily configured to handle static websites. Right now, both this blog & the [Pocket Dogfights](http://www.pocketdogfights.com) website site are active via S3 (with the blog hosted in Amazon's Sydney environment, and the Pocket Dogfights one in their California one).

Judging from the performance alone, it's been well worth it - what I can't wait to see is the resultant bills, going with S3 for hosting allows for some incredibly cheap rates for traffic, and combined without the need to manage configurations for Apache (or your preferred web server), it means that my infrastructure set up is simplified that little bit. Joy.
