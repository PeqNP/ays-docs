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

## Create a Custom Node Property

If you are creating your own template measurements, interfaces, etc. you may need a custom node property. To do this:
- Navigate to the template node that contains the template measurement(s)
- Tap the `Properties` row
- Tap on the `Add property` button

It will ask you for the "name" of your custom property. This property name should have no spaces and contain values between `a-zA-Z0-9_`. At Bithead we use snake cased variable names.

Please note that custom properties can be applied to any node type. However, there are currently no use cases for non-template nodes to have them. It is better to assign static value(s) to a script's parameters in these contexts.
