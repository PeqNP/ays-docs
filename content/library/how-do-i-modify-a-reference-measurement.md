---
title: "How Do I Modify a Reference Measurement"
date: 2022-11-05T07:33:56-07:00
draft: false
---

# How do I modify a Reference Measurement?

Reference measurements inherit another measurement's configuration. Therefore, they can not be edited directly. To update the configuration used by a reference measurement, you must update the configuration on the measurement it references.

As an example, imagine you are viewing a list of measurements on a node. A reference measurement will display a message, "Reference measurement to `com.example.service`". To update this reference measurement's configuration, you must modify the respective measurement that is associated to the `com.example.service` node.
