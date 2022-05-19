---
title: "Using cached responses"
description: "Learn how to use past responses to build requests"
draft: false
images: []
weight: 120
toc: true
---

`hit` caches responses from each request execution and elements of the
response can be used to construct new requests using
[request templates]({{< relref "request-templates" >}}).
In this guide, we will go through some examples of how to use `hit`'s cache
to construct requests.


## Referencing cache in the template

Let's start with a basic example:

```bash
echo '
@_global
base_url=https://nodes.yolo42.com
version=1


@gen-root-node
POST
/v1/node
~y2j
title: "root-node"

@create-node
POST
/v1/node
~hy2j
title: "child-node"
parent_id: "@gen-root-node.id"
' > quick-start.hit
```

In this example, there are two requests:
- `@gen-root-node` has a static YAML body. There is nothing special about it.
- `@create-node` is a request template where `parent_id` refers to `id` key
  from the response of `@gen-root-node` request.

Let's go ahead and take a look at how this works out.

Create a root node:
```bash
hit @gen-root-node
```

and then create a child node:

```bash
hit @create-node
```

If you observe, you can see that the parent_id of the child node matches
with the id of the root node.

In this way, a template can reference response from any other request.

## Dynamic cache references

Even though static cache references can enable a variety of
workflows, the real power of cache referencing comes when one combines them
with CLI arguments and
[request templates]({{< relref "request-templates" >}}).

Let's take an example:

```bash
echo '
@_global
base_url=https://nodes.yolo42.com
version=1


@gen-root-node
POST
/v1/node
~y2j
title: root-node


@get-node
GET
/v1/node/@2

@create-node
POST
/v1/node
~hy2j
title: "@2"
parent_id: "@3"
' > quick-start.hit
```

Let's create a root node:

```bash
hit @gen-root-node
```

And then, to create a child node:

```bash
hit @create-node "child-0" @gen-root-node.id
```

Did you see what just happened?
Variable resolution is happening at two layers:
- The `title` field in `@create-node` references `@2`, a CLI argument.
- The value of `@2` above is `@gen-root-node.id` which resolves to the `id`
  field of the response of `@gen-root-node` request execution.

You can read back the parent node in one of two ways now:

```bash
hit @get-node @gen-root-node.id
# or
hit @get-node @create-node.parent_id
```


Let's create a couple of grandchild nodes:

```bash
hit @create-node "grandchild-0" @create-node.id
```

And then one more:

```bash
hit @create-node "grandchild-1" @create-node.parent_id
```

Now, let's read the `child-0` node:

```bash
hit @get-node @create-node.parent_id
```

You can combine and reorder request execution in this fashion to accomplish
complicated workflows. The possibilities are endless!
