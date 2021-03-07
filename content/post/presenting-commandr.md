---
title: 'Presenting commandr: an easy to use and automatic CLI builder for Python'
date: 2013-05-23
draft: true
---
*This article was originally published to the TellApart Engineering Blog on 2013–05–23*

Scripts are a big part of any code base, and if you’re like us, you have lots of them. Also, if you’re like us, you’re not too fond of writing Python optparse specifications. That’s why we created [commandr](https://t.umblr.com/redirect?z=https%3A%2F%2Fgithub.com%2Ftellapart%2Fcommandr&t=YzFhNjQxNTk3ZjgwZTk1MjEzMzExZmMxODY0OTIzNzU5MzYzZWY5MixoTnBSUVNqSQ%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F51142273614%2Fpresenting-commandr-an-easy-to-use-and-automatic&m=1), a tool for automatically converting a function’s signature into a command line interface, using just a decorator. We’ve found commandr so useful, we decided to open-source it!

commandr has a number of useful features:

* It infers and casts types automatically from default values.

* Documentation is automatically generated from each function’s signature and docstring.

* Boolean parameters are automatically converted to flags, (e.g. –caps or –no_caps).

* Commands can be grouped, making long lists of commands easy to read.

Here’s an example usage:

<iframe src="https://medium.com/media/aa9ba25350f42585e2c0d3bc829b9f5c" frameborder=0></iframe>

From the command line:

<iframe src="https://medium.com/media/cd8a72daa8e0f68a9505aae8275152b8" frameborder=0></iframe>

Internally, we’ve combined commandr with [fabric](https://t.umblr.com/redirect?z=http%3A%2F%2Ffabfile.org&t=M2YwNGEzNGRlZmJlZTIzMzE5ZWM1NzlhOGUzM2Y4ZmQ3MDg0MTQyMCxoTnBSUVNqSQ%3D%3D&b=t%3AtSukOFSuQs_w3dGZQMwq8Q&p=http%3A%2F%2Ftellaparteng.tumblr.com%2Fpost%2F51142273614%2Fpresenting-commandr-an-easy-to-use-and-automatic&m=1) to allow functions to be invoked from our local command lines and executed on remote servers — just by adding a decorator. (Unfortunately, that part was too tightly integrated with the rest of the TellApart stack to release it here).

You can get commandr right from PyPI:

<iframe src="https://medium.com/media/87b53bbb67d25f84b2d409b5af07b4b0" frameborder=0></iframe>

Hopefully, you’ll find this tool as useful as we do!