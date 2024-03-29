---
title: "What Is a Template Node"
date: 2022-10-12T06:53:57-07:00
draft: false
---

# What Is a Template Node?

A template node is designed to represent a *type* of system in your organization. You use them to monitor *like* systems in the same way.

Template nodes can also be used to build a library of utility functions. For example, Bithead has several utility template nodes such as `com.bithead.template.ping` and `com.bithead.template.query`. These provide common utilities that many other nodes may find useful. No coding required!


For example, imagine you have a group of services that send data to New Relic. Let's also imagine that their health can be monitored in the same way. Each service can be identified by the `host` they are running on. You will then write a NRQL query that can be used to determine the health of the `host`. Sensor scripts allow you to accept this `host` value as a parameter to your sensor function. You can then interpolate the `host` value into your NRQL query, query New Relic, and return the respective data point for that service.
