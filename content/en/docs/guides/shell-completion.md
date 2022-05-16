---
title: "Setup shell completion"
lead: "Learn how to set up shell completion"
description: "Learn how to set up shell completion"
draft: false
images: []
weight: 110
toc: true
---

Using `hit` with shell completions reduces the number of keystrokes required
to execute a request by an order of magnitude.

To enable shell completion in your current shell:

```bash
source <(hit completion)
```

Once enabled, press `TAB` to get a recommendation for all available request
identifiers in the current working directory.

To set up completion permanently, please follow the instructions
specific to your shell:

# Bash

```bash
echo '
# enable shell completions for hit command
# https://hit.yolo42.com
source <(hit completion)
' >> ~/.bashrc
```

# Zsh

```bash
echo '
# enable shell completions for hit command
# https://hit.yolo42.com
source <(hit completion)
' >> ~/.zshrc
```

If you are using `hit` with another shell and would like auto-completion
support, please open a [feature request](https://github.com/hbagdi/hit/issues)
with us.
