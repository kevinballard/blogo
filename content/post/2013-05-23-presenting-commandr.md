---
title: 'Presenting commandr: an easy to use and automatic CLI builder for Python'
date: 2013-05-23
draft: false
---
*This article was originally published to the TellApart Engineering Blog on 2013–05–23*

Scripts are a big part of any code base, and if you’re like us, you have lots of them. Also, if you’re like us, you’re not too fond of writing Python optparse specifications. That’s why we created [commandr](https://github.com/kevinballard/commandr), a tool for automatically converting a function’s signature into a command line interface, using just a decorator. We’ve found commandr so useful, we decided to open-source it!

commandr has a number of useful features:

* It infers and casts types automatically from default values.

* Documentation is automatically generated from each function’s signature and docstring.

* Boolean parameters are automatically converted to flags, (e.g. –caps or –no_caps).

* Commands can be grouped, making long lists of commands easy to read.

Here’s an example usage:

{{< highlight python >}}
from commandr import command, Run

@command('greet')
def Hi(name, title='Mr.', times=1):
  '''Greet someone.

  Arguments:
    name - Name to greet.
    title - Title of the person to greet.
    times - Number of times to say the greeting.
  '''
  greeting = 'Hi %s %s!' % (title, name)
  for _ in xrange(times):
    print greeting

if __name__ == '__main__':
  Run()
{{< /highlight >}}

From the command line:

{{< highlight text >}}
$ python example.py
> Command must be specified
>
> General Commands:
>   greet

$ python example.py greet
> All options without default values must be specified
>
> Current Options:
>  --name=None
>  --title=Mr.
>  --times=1
>
> Documentation for command 'greet':
> ----------------------------------------
> Greet someone.
>   Arguments:
>     name - Name to greet.
>     title - Title of the person to greet.
>     times - Number of times to say the greeting.
> ----------------------------------------
>
> Usage: example.py command [options]
> Options without default values MUST be specified
>
> Options:
>   -h, --help
>   -n NAME, --name=NAME
>   -t TITLE, --title=TITLE
>                           [default: "Mr."]
>   --times=TIMES           [default: 1]

$ python example.py greet --name Smith
> Hi Mr. Smith!

$ python example.py greet John --times blah
> Usage: example.py command [options]
> Options without default values MUST be specified
>
> example.py: error: option --times: invalid integer value: 'blah'

$ python example.py greet Nick Dr. --times 2
> Hi Dr. Nick!
> Hi Dr. Nick!
{{< /highlight >}}

Internally, we’ve combined commandr with [fabric](http://fabfile.org) to allow functions to be invoked from our local command lines and executed on remote servers — just by adding a decorator. (Unfortunately, that part was too tightly integrated with the rest of the TellApart stack to release it here).

You can get commandr right from PyPI:

{{< highlight bash >}}
$ pip install commandr
{{< /highlight >}}

Hopefully, you’ll find this tool as useful as we do!
