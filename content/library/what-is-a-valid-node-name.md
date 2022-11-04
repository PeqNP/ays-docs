---
title: "What Is a Valid Node Name"
date: 2022-11-04T14:03:49-07:00
draft: false
---

# What Is a Valid Node Name?

At times, the system may emit a warning stating that you have provided an invalid node name. Here are the rules **@ys** uses to determine if a node name is valid:

- A node name must be at least one character
- A node name must be all lowercase. In most contexts, this is done for you automatically.
  - More specifically, a node name must be within the range of characters `a-z0-9_-`
- A node name must be within the range of characters `a-z`
- A node name may not be a reserved name. As of today, the reserved names are `measurements`, `c`, and `xff`.
