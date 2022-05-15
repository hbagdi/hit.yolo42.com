---
title: "Quick Start"
description: "A summary of how to use hit."
lead: "A summary of how to use hit."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "prologue"
weight: 110
toc: true
---

## Install hit

### macOS

```bash
brew install hbagdi/tap/hit
```

### Linux

Grab the binary from the release page and install:

```bash
curl -sL https://github.com/hbagdi/hit/releases/download/v0.1.0/hit_0.1.0_linux_amd64.tar.gz -o hit.tar.gz
tar -xf hit.tar.gz -C /tmp
sudo cp /tmp/hit /usr/local/bin/
```

## Verify hit is installed correctly

```shell
hit version
```

It should output the version of hit that is currently installed on your system.

## Create your first hit file

Create a hit file using the following command:

```shell
echo '
@_global
base_url=https://httpbin.org
version=1


@c0
GET
/headers
foo: bar
baz: qux
' > quick-start.hit
```

The above file defines a couple of things:

- `@_global` section defines hit settings that apply to all files in the
current directory. Two global properties are defined, `base_url` and `version`.
All requests are constructed on top of the `base_url`. `version` is the
version of the hit file - the only valid version is 1.
- `@r0` section defines an HTTP request with an ID of `r0`. The line after
the ID, in this case 'GET' defines the
[HTTP method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
used to construct the request. Next line is the HTTP request line, popularly
known as the HTTP path of the request. Lines after the path are HTTP headers for
the request.

With that bit of background, let's go ahead and hit your first HTTP request:

```shell
hit @c0
```

The above command instructs hit to load all files in the present workibng
directory and initiate the `c0` request.
The request and response are printed on the screen. It should look something
like:

```shell
GET /headers HTTP/1.1
Host: httpbin.org
User-Agent: Go-http-client/1.1
foo-header: bar
Accept-Encoding: gzip


HTTP/1.1 200 OK
Content-Length: 216
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
Connection: keep-alive
Content-Type: application/json
Date: Wed, 30 Mar 2022 04:18:33 GMT
Server: gunicorn/19.9.0

{
  "headers": {
    "Accept-Encoding": "gzip",
    "Foo-Header": "bar",
    "Host": "httpbin.org",
    "User-Agent": "Go-http-client/1.1",
    "X-Amzn-Trace-Id": "Root=1-6243da19-708fb5131135b2582a339aaa"
  }
}
```

Congratulations! You hit your first HTTP request successfully.


### Enable auto-completion

Let's first enable shell auto-completion to save some keystrokes.

```shell
source <(hit completion)
```

You can type `hit` and press the `TAB` key to see suggestions.
In the above file, there is only request so your shell will automatically
complete the prompt to `hit @c0`.


## An advanced example - Nodes API

Next, let's grab a hit file that does more than a `GET` request.

```shell
curl --silent https://hit.yolo42.com/quick-start.hit --output quick-start.hit
```

Create a root node for the tree using hit.

```shell
hit @gen-root-node
```

Next, we are going to create a child node under the root node:

```shell
hit @create-node "buy-groceries" @gen-root-node.id
```

In the above command, the parameter `@gen-root-node.id` references the
`id` field from the latest response body of the `@gen-root-node` request.

Let's create another node under the node that we just created.

```shell
hit @create-node "tomatoes" @create-node.id
```

Let's take a look at tour grocery list.

```shell
hit @get-node @create-node.parent_id
```

Let's go ahead and add a couple of items.

```shell
hit @create-node "potatoes" @get-node.id
hit @create-node "milk" @get-node.id
```

Let's grab our grocery list now.

```shell
hit @get-node @get-node.id
```

Let's delete an item, let's delete the first item in the grocery list.

```shell
hit @delete-node @get-node.children.0.id
```

Grab the grocery list again

```shell
hit @get-node @get-node.id
```
