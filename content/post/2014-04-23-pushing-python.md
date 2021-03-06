---
title: 'Pushing Python: Building a High Throughput Distributed System'
date: 2014-04-23
draft: false
---
*This article was originally published to the TellApart Engineering Blog on 2014–04–23*

Just under 2 years ago [we open-sourced Taba](http://tellaparteng.tumblr.com/post/49814523799/taba-low-latency-event-aggregation) — our distributed instrumentation and event aggregation service. Since then we’ve scaled up our deployment from handling 10M events/minute to 10M events/**second** (and at a lower latency for good measure). To get there though required rethinking some of the underlying architectural decisions, which necessitated a rewrite of the core Taba Server.

The rewrite was well worth the effort though. Besides the order of magnitude higher throughput, we added several highly requested features:

* Cluster auto-discovery and auto-balancing

* Support for Redis Sentinel, including database discovery and automatic failover

* Regular expression queries on Tab Names and Client IDs

* Query caching, which improves response times for the most common large queries from multiple minutes to just a couple seconds

* Pluggable Type Handlers

* Support for “super-aggregates” that can arbitrarily aggregate any Tabs of the same type

* Standard Python deployment tools and availability on PyPi

We found all these improvements so useful that we wanted to share them. So today we’re announcing the [release of Taba v0.3](https://github.com/tellapart/taba/tree/release-0.3.4), which is the latest version TellApart is running internally. Also, we’re moving our entire internal deployment of Taba onto the public version, and all new development will occur in the public repository. This means that all future improvements will be automatically available to the broader community.

Additionally, we’re releasing a [Java version of the Taba Client](https://github.com/tellapart/taba-java-client) library, so you’re no longer limited to instrumenting just Python processes.

## 4 Lessons Learned

In the process of building Taba v0.3, we learned a lot about scaling a distributed service in Python. Some of the more interesting lessons were:

### 1. Think carefully about your data model

The way a problem is modeled informs what a solution is capable of, and subtle differences in the model can have dramatic effects on performance. In Taba, we made a small change in the way States are aggregated into query responses, which made aggressive caching possible. This in turn decreased response times by several orders of magnitude.

### 2. Maintaining state is hard

Maintaining consistent and durable state is one of the fundamental problems of computer science. Fortunately we have existing tools (like Redis) that we can lean on to solve this problem for us. Taba consists of a small central cluster of Redis instances that comprise a hardened sub-service for maintaining all state. The rest of the Taba Server workers are stateless, and can be added or removed from the cluster seamlessly. That makes Taba highly resistant to failures, and trivially easy to scale up or down.

### 3. Generators and greenlets work well together

A pattern that comes up again and again in Taba is the combination of generators and greenlets to create just-in-time processing pipelines. It’s a powerful abstraction that makes coordinating complex processing significantly simpler.

### 4. CPython suffers from memory fragmentation

The CPython interpreter has trouble managing memory for long running processes that handle a high throughput of data, especially if that data is a combination of large and small objects. Taba uses several techniques to avoid memory fragmentation, including using generators to reduce in-flight objects, allocating critical blocks of memory manually to control placement and deallocation, and avoiding persistent objects that can cause heap ratcheting.

I recently had the opportunity to talk about these points in a bit more detail at **PyCon 2014 in Montreal**. The [slides](https://speakerdeck.com/pycon2014/pushing-python-lessons-learned-building-a-high-throughput-service-in-python-by-kevin-ballard) and a video of the talk are available online:

{{< slideshare id="33870076" >}}

{{< youtube k8YtaSMv-Nc >}}

The entire conference was jam-packed with information — I think I learned more about state-of-the-art Python in 3 days than I have in the last year. All the talks have been put online at [pyvideo.org](http://www.pyvideo.org/); you should definitely check them out!