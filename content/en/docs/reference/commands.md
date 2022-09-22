---
title: "Commands"
description: "Commands in the hit program"
lead: "Commands in the hit program"
date: 2020-10-13T15:21:01+02:00
lastmod: 2020-10-13T15:21:01+02:00
draft: false
images: []
menu:
  docs:
    parent: "prologue"
weight: 72
toc: true
---

hit's goals is to be as simple and intuitive to use as possible.
And in that spirit the number of command that hit supports is fairly small.
For hitting HTTP requests, `hit` followed by the request identifier (for
example `@foo`)
should be sufficient.

For other features, there are a few other commands available:

## browse


## version

Output the version of the hit command.

For example:

```bash
hit version
```

## completion

Output the shell completion script for hit.

```bash
hit completion
```

Typically, you would do something like the following to enable bash
completion for your shell.

```bash
source <(hit completion)
```
