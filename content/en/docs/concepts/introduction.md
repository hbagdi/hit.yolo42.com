---
title: "Introduction"
description: "hit is a command to manage and make HTTP requests."
draft: false
images: []
weight: 91
toc: true
---

Hit lets you express complex HTTP requests in simple formats and create
workflows out of these requests. It allows you to express complex requests as
composition of responses from previous HTTP requests.

Hit was born out of frustration with using the `history` command to look up
`curl` invocations. For folks working with HTTP-based APIs, this is probably a
relatable experience. Tracking  requests in your shell history works, but it
becomes cumbersome to fetch the previous requests reliably and quickly.

Hit takes a new approach to making and managing such requests. All requests
and responses are tracked and templates out of requests can be made easily.
Because of the text-based nature of request formats, request templates can
be created quickly using a text-editor of choice. Request templates allow
for input during execution as well as referencing of values from response of
any past request execution. The templates can then be mixed and matched to
execute complex request patterns quickly.
