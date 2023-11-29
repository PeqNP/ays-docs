---
title: "How Is Node Health Determined"
date: 2022-10-12T08:12:59-07:00
draft: false
---

# How Is Node Health Determined?

A node's health is determined by averaging all of the health values of its monitors, children, dependencies, and external system monitors.

If a node's health changes, those changes will be propagated and affect the health of all of its dependents and parents. The algorithm walks backwards up the system graph until it reaches each organization node.

For example, if a node (which will we refer to as node "A") is a dependency to node "B", then node B's health will be affected by node A's health by virtue of it being dependent on node A.

```
Node A Monitor with `Warning` state -> affects Node A health
  -> affects Node A parent health
  -> affects Node B health (because it's dependent of A)
  ...
  -> affects all other nodes which are a parent, or dependent, of node A and B up until the TLD nodes
```
