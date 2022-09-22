---
title: "Defining request templates"
description: "Learn how to define request templates"
draft: false
images: []
weight: 120
toc: true
---

Request templates are a core part of `hit`. Request templates are a
"functional" approach to APIs.
In this guide, we will go over how to create and use request templates.

## Basics

At its core, templates allow for injection of dynamic values into a request.
A template provides a structure of a request and places where variable-based
substitution can be performed.

Please make sure that no `.hit` files are present in your current working
directory. Create a new directory if necessary.

Let's start with a basic request:

```bash
echo '
@_global
~
base_url=https://nodes.yolo42.com
version=1
~


@gen-root-node
POST /v1/node
~y2j
title: root-node
~
' > quick-start.hit
```

`@gen-root-node` defines a POST request. The body format is `y2j` meaning
the request is defined as a YAML document in the hit file, and it is sent as
JSON in the HTTP request. The title here is hard-coded to 'root-node'. Let's
make it dynamic by introducing a variable.

```bash
echo '
@_global
~
base_url=https://nodes.yolo42.com
version=1
~


@gen-root-node
POST /v1/node
~y2j
title: "@1"
~
' > quick-start.hit
```

Notable change is that the value of `title` key in the body has changed
from `root-node` to `@1`. The numeric value `1` indicates that the first
argument from the command-line should be used as the value. The CLI arguments
are 1-indexed. The zeroth argument of the program the request ID which is
`@gen-root-node` in this case and.

Let's execute the request:

```bash
hit @gen-root-node foobar
```

Observe how the request body (as well as the response) has `foobar` as the
`title`.

## Multiple input values

You can input multiple values using the CLI as well.

Let's take another example:

```bash
echo '
@_global
~
base_url=https://nodes.yolo42.com
version=1
~


@gen-root-node
POST /v1/node
~y2j
title: "@1"
~

@create-node
POST /v1/node
~y2j
title: "@1"
parent_id: "@2"
~
' > quick-start.hit
```

Here the `@create-node` request takes two inputs - a title and a parent_id.

Generate a root node:

```bash
hit @gen-root-node "Todo list"
```

Copy the id from the reponse and then create another node:

```bash
hit @create-node "Buy milk" "<id from previous request>"
```

## Dynamic injection from cache

Copying output of a request and pasting it into a command is quite unwieldy.
To  make this easy, `hit` has caching of responses and referencing responses
from templates as well as on the command line.
This allows to quickly execute complex series of requests.
To learn more, please follow the
[Using cached responses]({{< relref "cached-responses.md" >}}) guide.
