---
title: "Quick Start"
description: "One page summary of how to use hit."
lead: "One page summary of how to use hit."
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

## Requirements

- Install hit. Please refer the [installation guide](/docs/install/install).

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
base_url=http://httpbin.org
version=1


@r0
GET
/headers
foo: bar
baz: qux
' > hello.hit
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
