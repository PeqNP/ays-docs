---
title: "How Is Node Health Computed"
date: 2023-02-18T10:33:39-08:00
draft: false
---

# How is Node Health Computed?

The **Node Health Page** is responsible for showing how the Node's health is computed.

The **Overall Health** is determined by averaging all of the health values of its monitors, children, dependencies, and external system monitors.

If a node's health changes, those changes will be propagated and affect the health of all of its dependents and parents. The algorithm walks backwards up the system graph until it reaches each organization node.

For example, if a node (which will we refer to as node "A") is a dependency to node "B", then node B's health will be affected by node A's health by virtue of it being dependent on node A.

```
Node A Monitor with `Warning` state -> affects Node A health
  -> affects Node A parent health
  -> affects Node B health (because it's dependent of A)
  ...
  -> affects all other nodes which are a parent, or dependent, of node A and B up until the TLD nodes
```

## Discrepency Messaging

Do see you see a message like this?

- "3 not found, 2 extra samples"
- OR "3 not found"
- OR "2 extra samples"

This indicates a discrepenancy between the object and its respective sample data. This should never happen. If it does, please contact us and we wil fix the issue.

