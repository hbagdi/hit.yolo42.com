---
title: "Changelog"
draft: false
images:
- images/change.jpg
weight: 74
toc: true
---

<img src="/images/change.jpg"  alt="change of leaf colour" width="100%"/>

## v0.3.0

> Released September x, 2022

This is a feature packed release with several breaking changes as the core of
hit gets ironed out.

### 🌋 Breaking changes:

All breaking change are in the `.hit` file formats and semantics:
- Request parameter input via positional argument now use 1-based indexing
  instead of 2-based indexing i.e. first parameter after the request ID is
  referenced using `@1` instead of `@2`.
- `hy2j` body encoding has been removed. Please instead use `y2j`. hit is
  capable of doing substitution within y2j format itself.
- Request bodies as well as `@_global` sections now must be closed using a
  `~` line. This change is intended to make hit files more expressive.
- `@_global` section is now YAML formatted.
- HTTP method and path are now consolidated into a single line instead of a
  separate line for a path and a line. This should be more intuitive as it
  is more similar to format of an HTTP request in RFC 2616.

### 🐣 Features

**Request log and sharing**: New command `hit browse` to browse all requests
executed using `hit` and `hit curl` and an option to share them. Please read
our [Using hit browser] and [Sharing requests] guides for further details.
These workflows make it easy to keep track of request executions and share
a simple curl requests with
colleagues.

**Use cURL with hit**: `hit` can run in the background with the introduction
of `hit curl` command. `cURL` has been around for decades and is more powerful
than `hit` can ever be. Big fans to be honest. Simply `alias curl='hit
curl'` and use curl as you normally use and all of your requests will be logged.
If you prefer to explicitly opt-in/out, you can `alias hcurl='hit curl'`.
Please read our [Using hit with curl](guides/using-hit-with-curl)  guide for
further details.

**SQLite storage engine**: Hit stores all HTTP requests and responses that have
been executed in the past in order to provide features like request chaining,
sharing of requests. Previously, the storage backend was a flat JSON file -
the flat file was quick and was sufficient for a PoC. Hit now has a more stable
and robust storage solution now. This lays the ground for some future
features as well as powers the `hit browse` command.

A slew of small features:
- `@_global` section now has a headers field for headers applicable to all
  request templates in the directory.
- Caller can now specify a custom user-agent to override the default `hit`
  user agent.
- Status line from HTTP response is now recorded in addition to HTTP status
  code.
- Additional validation is performed for `base_url` in the `@_global`
  section to ensure validity of requests.
- Redirects are not automatically followed. There is no way to currently
  re-enable this feature.


### 🐞 Fixes

- `content-type` header is correctly set for `y2j` body encoding. If no
  body-encoding is specified, the caller is responsible for specifying the
  `content-type` header.
- HTTP headers are now sorted.
- Error messages for non-existent request IDs have been improved. They
  should be less cryptic.
- `host` HTTP-header is now correctly populated before sending the request.

## v0.2.0

> Released May 20, 2022

This is a bit more usable version of `hit`.
It is intended to give you a feel of the product and its vision.

Features that are supported:
- Core hit request workflow works for HTTP requests
- Request templates for re-usable requests
- Caching of responses and

## v0.1.0

> Released March 25, 2022

The first!
Most things didn't work in this version.
