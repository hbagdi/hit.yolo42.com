---
title: "hit v0.3 - use hit with cURL and share HTTP requests/response with others"
description: "Introducing Hit v0.3, a tool to make and manage HTTP requests."
lead: "Introducing Hit v0.3, a tool to make and manage HTTP requests."
date: 2022-08-05T09:19:42+01:00
draft: false
weight: 50
contributors: ["Harry Bagdi"]
---

## Features

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

