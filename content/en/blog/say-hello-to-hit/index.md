---
title: "Say hello to Hit 👋"
description: "Introducing Hit, a tool to make and manage HTTP requests."
lead: "Introducing Hit, a tool to make and manage HTTP requests."
date: 2022-06-05T09:19:42+01:00
draft: false
weight: 50
contributors: ["Harry Bagdi"]
---

I'm stoked to announce the launch of Hit - a command line tool to manage HTTP
requests. Hit takes a command-line first approach to managing HTTP requests,
executing them and sharing them with others.

## Demo-time

Nothing beats a demo!

<script id="asciicast-p53Tfk58IZv25HqLQAxwMZiWR" src="https://asciinema.org/a/p53Tfk58IZv25HqLQAxwMZiWR.js" async></script>

## Why build a new tool?

I spend the majority of my time on the terminal and write backend software.
To execute requests, I usually resort to `curl` or similar programs, which
evolve into scripts - shell or python. Such scripts typically get out of hand as
I'm looking for something quick that solves the problem at hand and don't
have the time to maintain and improve them.
Another problem is that when I want to find a `curl` that I executed some
time ago, doing a `history | grep curl ...` yields nothing. Either I can't
remember the command I executed, or it is far too cumbersome to search the
history. I need a tool that is programmable, fast and works over
long-periods of development time as the number and complexity of requests
scales well beyond the limits of my ability to remember all the knobs.

The same problem becomes much more complicatd with team projects. One engineer
starts with a script, these get out of hand as everyone wants to customize some
different parts of the request. Again it is rare for these scripts to receive the
attention and care that they need. These scripts also get peppered with choices
and styles of other engineers - which has its up and down.
As new engineers onboard, they have to spend time looking through the
scripts or code to figure out how to execute a specific request that they
need to finish the task at hand - such as debugging a specific endpoint or
adding a feature to a set of endpoints.

HTTP is the foundation of most modern APIs - from banking to shipping and
API-based HTTP requests make over 80% of the web traffic. Yet, I find that the
tooling to manage HTTP requests is poor and can be improved significantly.
I believe that the simplicity of the HTTP protocol is a big reason for its
success. We need a tool that is equally simple to make it more manageable as the
building blocks on top of HTTP become more and more complex.

I should acknowledge here that there are a lot of GUI-based apps in the
market that try to solve problem in this area, and they do an amazing job.
GUIs are great but I need something that focuses on the terminal.
hit is all about a superior CLI experience.
There is nothing wrong with GUI-based apps - they don't work for
me as I prefer sticking to the terminal for most of my work.

`hit`'s goal is to make executing requests easy, keep track of the executed
requests, their responses and when the need arises, share the requests with
others - all from the terminal.

## Progress so far

What is being launching today is a very rough and an
[early MVP](https://medium.com/galleys/the-minimum-viable-product-a-primer-3d9a76dd5213)
with a lot of rough edges. One can write HTTP requests using text files and
then execute those requests.
In terms of features, only the most basic features are present at the moment.
I expect most users to run into issues and some bugs could be
surprisingly embarrassing. The goal is to get some early feedback from the
hit's early adopters.

Please give hit a try using the
[quick-start-guide][quick-start-guide].
If you run into issues or have any feedback, please open a
[Github issue](https://github.com/hbagdi/hit/issues), I would love to hear
whatever you have to say.

## Path forward

While I'm still figuring out details, I've an exciting roadmap planned for hit.
Some planned features include advanced search of historical executions,
browsing of requests, sharing features, and most importantly compatibility
with existing popular command line tools like curl.

If you have ideas or feedback, please reach out!

If you like the vision, please star hit's Github repository
[hbagdi/hit](https://github.com/hbagdi/hit, follow
[@hitcmd](https://twitter.com/hitcmd) and share this blog with someone who
may be facing a similar problem

Stay tuned for features and a more complete program.
Thank you and keep it simple!

[quick-start-guide]: /docs/get-started/quick-start
