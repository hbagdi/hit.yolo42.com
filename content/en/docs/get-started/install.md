---
title: "Install hit"
description: "Install hit"
draft: false
images: []
weight: 101
toc: true
---

Hit is a single binary program and extremely easy to install.
Below are installation instructions based on your Operating System (OS):

## macOS

```bash
brew install hbagdi/tap/hit
```

## Linux

Grab the binary from the release page and install:

```bash
curl -sL https://github.com/hbagdi/hit/releases/download/v0.1.0/hit_0.1.0_linux_amd64.tar.gz \
  -o /tmp/hit.tar.gz
tar -xf /tmp/hit.tar.gz -C /tmp
sudo cp /tmp/hit /usr/local/bin/
```


## Verify hit installation

```bash
hit version
```

The command will print the version of hit installed on your system.

## Using hit

Once installed, please head over to the
[quick-start guide]({{< relref "quick-start" >}}) to execute your first
request.
