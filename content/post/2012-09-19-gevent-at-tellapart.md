---
title: gevent at TellApart
date: 2012-09-19
draft: false
---

This article was originally published to the TellApart Engineering Blog on 2012–09–19

At TellApart, we’re big fans of [gevent](http://www.gevent.org). It powers a number of our core components, from the [TellApart Front End](http://tellaparteng.tumblr.com/post/49818501891/tellapart-frontend) servers, to our open-source [Taba](http://tellaparteng.tumblr.com/post/49814523799/taba-low-latency-event-aggregation) aggregation service. For those not familiar with it, gevent is a library for standard Python (CPython) based on [greenlet](http://greenlet.readthedocs.org/en/latest/index.html) and [libevent](http://libevent.org/), which enables high concurrency workloads and co-operative scheduling.

Since we use it so extensively, we were recently invited to give a talk at [Pinterest](http://pinterest.com) about gevent, its advantages, some pitfalls to avoid, and how we use it throughout the TellApart stack. We wanted to share the slides from that presentation for anyone who’s interested.

{{< slideshare id="14351232" >}}
