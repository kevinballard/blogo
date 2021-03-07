---
title: 'Taba: Low Latency Event Aggregation'
date: 2012-03-20
draft: false
---
*This article was originally published to the TellApart Engineering Blog on 2012–03–20*

**Introduction**

At TellApart we love metrics, and certainly have lots to measure. We track data for over 20,000 different event types across all parts of our stack (and that’s just the real-time data!). This information is used for all sorts of things, like monitoring, performance metrics, segmentation information, and feedback loops. In order to manage all this data, we created the Taba service (the name is derived from the Japanese for bundle or flux (束)).

In designing Taba, we had a number of goals:

* **Low latency**: An event should be visible within seconds of occurring. This enables responsive monitoring, tight feedback loops, and other near-line applications.

* **Low impact**: CPU and memory usage within the client applications should be minimized.

* **Durability**: Events should be reasonably durable, so that a Taba “Tab” can be used as a basis of important services like monitoring.

* **Scalability**: All components of the Taba service should be horizontally scalable to keep up with the applications it tracks.

**Different Types**

Each event type, or “Tab”, being tracked is identified by a Name, and a Type that maps to a Handler class. The core Taba service doesn’t implement data manipulation operations — all schemas and transformations are left to Handlers. By separating the schemas from the rest of the service, Tabs that behave differently can easily co-exist, and implementing new types of aggregation is simple.

**Data Model**

The fundamental element of data in the Taba service is the Event. Events are composed of three pieces of data: the Tab, the time, and a value. Events are gathered to a central server (more on this later), and combined into State objects which are persisted in a database. The motivation behind persisting States instead of the individual Events is two-fold: (1) storing all events would consume far too much space (timestamps alone would consume gigabytes per hour), and (2) pre-calculated State objects mean faster query response times.

When the Taba service is queried, States are converted into Projections and/or Aggregates. A Projection is a reduction of the State into a dictionary, and an Aggregate is a combination of Projections. Depending on the query, a Projection or an Aggregate will be returned, optionally rendered by the Handler into a human-readable format.

**Architecture**

Applications generate Events by embedding a Taba Client. The Client briefly buffers Events and posts them to a Taba Agent over an HTTP based protocol. An Agent receives Events from multiple Clients (usually on the same machine) briefly buffers them, and posts them to the Taba Server using the same protocol. The Client + Agent scheme allows for a very simple and resource-light Client, putting more complex buffering and durability functions in a separate process. The Agent also helps performance by batching requests to the Server.

The Server is where the real magic happens. Like [TellApart’s TAFE server](https://tellaparteng.tumblr.com/post/49818501891/tellapart-frontend), it’s a distributed Python service sitting behind an Nginx reverse proxy, and uses [gevent](http://www.gevent.org) for simple and fast co-operative concurrency. The Server itself is stateless, meaning you can launch as many as needed; the Agents will distribute requests across Servers. The Server receives Events and invokes the appropriate Handler to fold them into States, or generate Projections and Aggregates. A State object is maintained for each Client and Tab combination, so that the status of any Client can be queried.

We use [Redis](http://redis.io) for the database, but with our own transparent sharding layer on top to overcome single process limitations. Sharding is based on virtual buckets, and supports a subset of Redis data-types, and transactions/locking. Like the Server, as many Redis processes as needed can be run, and re-sharding without downtime is possible.

**In Production**

Currently, we have the Taba service deployed in each region as a cluster of 2 Servers instances and 1 Database instance, each running 8 processes. Each cluster handles over 10,000,000 events per minute, from 300 individual Clients across 20,000 different Tabs, with an average latency of 30 seconds. The Taba architecture and data model have allowed us to use it for fine-grained monitoring, real-time feedback systems, and internal Dashboards. We’ve only started to integrate its full functionality, and already it has provided a deeper insight into TellApart’s system.