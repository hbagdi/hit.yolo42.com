---
title: "Hit files"
draft: false
weight: 92
toc: true
---

`hit` files are at the center of `hit` command.
Request templates and parameters are defined using text files and then used
during command execution to send requests.
`hit` files can be edited like any other file containing code, and it is
friendly to SCM tools like `git`.
The files can be shared with colleagues and users to collaborate.

## Basics of hit file

Let's take a look at a basic hit file.
```
# demo.hit
# Lines starting with '#' are comments.

# `@_global` indicates a global section.
# A directory containing .hit files must have exactly one @_global section.
# Global section defines properties that apply to all requests
# within the parent directory.
@_global
~
base_url=https://httpbin.org
# `version` defines the format version of `.hit` files itself.
version=1
~


# Each request definition begins with an identifier definition.
# The identifier - `@c0` in this case - must be unique and is used to
# reference the request template and historical executions based on the
# template.
@c0
# This line defines the HTTP method and path for the request. Required.
GET /headers
# One or more headers. Optional.
foo: bar
baz: qux


# Another request. At least one empty line must be present between two
# subsequent requests.
@c1
POST /post
foo-header: bar
# Line beginning with `~` tells `hit` how to read the body. `y2j` format
# instructs hit to read the body as YAML and send it as JSON in the request
# to the server.
~y2j
# lines containing the body of the request
name: hit
description: make and manage HTTP requests
url: https://hit.yolo42.com
~
# body ends on the close `~`


## And so on
```

## Multiple hit files and directories

`hit` command automatically loads up all `.hit` files from the current
working directory. No additional flags or commands have to be specified to
load `hit` files. `hit` does not read `.hit` files from subdirectories.
