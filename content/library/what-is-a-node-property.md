---
title: "What Is a Node Property"
date: 2023-03-23T14:35:04-07:00
draft: false
---

# What Is a Node Property?

Every node has properties such as its `id`, `name`, and `path`. A node may also have custom properties. Properties are used by measurement sensors, interfaces, and actions.

For example, imagine you have created a measurement sensor that is driven by a Python script. The value of the node property can be interpolated as one of the script's parameters.

Below is an illustration of the relationship between a node property and how it is interpolated into a sensor Python script.

![Node Measurement Graphs](/help/img/node-property-relationships.png)

When this script is executed, it will take the value of `www.zonar.com` and pass it as the value for `host` in the `main` function.
