---
title: "How Do I Modify a Reference Monitor"
date: 2022-11-05T07:33:56-07:00
draft: false
---

# How do I modify a Reference Monitor?

Reference monitors inherit another monitor's configuration. Therefore, they can not be edited directly. To update the configuration used by a reference monitor, you must update the configuration on the monitor it references.

As an example, imagine you are viewing a list of monitors on a node. A reference monitor will display a message, "Reference monitor to `com.example.service`". To update this reference monitor's configuration, you must modify the respective monitor that is associated to the `com.example.service` node.
