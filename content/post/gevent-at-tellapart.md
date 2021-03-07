---
title: gevent at TellApart
date: 2012-09-19
draft: true
---

This article was originally published to the TellApart Engineering Blog on 2012–09–19

At TellApart, we’re big fans of [gevent](https://t.umblr.com/redirect?z=http%3A%2F%2Fwww.gevent.org%2F&t=YmJhNzlkZDliNjhkN2ExZTg5YzAwZWVjMjA1ZDkwYmE1ODJlMjIxMixlV1lQTUtsYg%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F49811368274%2Fgevent-at-tellapart&m=1). It powers a number of our core components, from the [TellApart Front End](http://tellaparteng.tumblr.com/post/49818501891/tellapart-frontend) servers, to our open-source [Taba](http://tellaparteng.tumblr.com/post/49814523799/taba-low-latency-event-aggregation) aggregation service. For those not familiar with it, gevent is a library for standard Python (CPython) based on [greenlet](https://t.umblr.com/redirect?z=http%3A%2F%2Fgreenlet.readthedocs.org%2Fen%2Flatest%2Findex.html&t=YjZkOWZiMGEyODI2ZmEwOWYxODM2MTNiOWVjYzcxYTk4ZWQ4ZTk0ZCxlV1lQTUtsYg%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F49811368274%2Fgevent-at-tellapart&m=1) and [libevent](https://t.umblr.com/redirect?z=http%3A%2F%2Flibevent.org%2F&t=NDY3Yjc5NzE1OTQzN2EwMmVlNGM0YmU0NmI5ZjJiN2E5M2I2MDYxYixlV1lQTUtsYg%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F49811368274%2Fgevent-at-tellapart&m=1), which enables high concurrency workloads and co-operative scheduling.

Since we use it so extensively, we were recently invited to give a talk at [Pinterest](https://t.umblr.com/redirect?z=http%3A%2F%2Fpinterest.com%2F&t=Y2NhNjk4NDM5ZWU2ZDI0NGJiOGRhZjlkMWFkM2VmNGRkMDkyODkwOSxlV1lQTUtsYg%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F49811368274%2Fgevent-at-tellapart&m=1) about gevent, its advantages, some pitfalls to avoid, and how we use it throughout the TellApart stack. We wanted to share the slides from that presentation for anyone who’s interested.

<iframe src="https://medium.com/media/0efa632639ef351e4b6377f70698ded8" frameborder=0></iframe>
