---
title: "Virtual Nodes"
date: 2022-03-13T22:06:59-07:00
draft: false
---

# Virtual Nodes

Virtual nodes are read-only nodes which inherit all properties from a template node. They may only be created, updated, or deleted from their parent node.

Virtual modes can be considered as ephemeral, although their life span depends on the context.

The typical use case for virtual nodes is that you wish to quickly assign the same measurements to many nodes. In other words, they represent an asset or service that share the same properties.

## Micro services

Imagine you have a micro service which can scale from 1 to N instances. Each instance must be managed the same way. At your service provides a public API that you can use to update the number of services in real-time. Now you can see the number of instances, and track the status of each micro service within *At Your Service*.

## Mobile app

Your company's mobile app consumes more than 30 external services. You need a way to track each of these 30 services in the same way. For instance, you may wish to track latency, requests per second, error rate, etc. Now you can easily easily track all of your services in the same way. If you find that some services need to be more finely tuned, convert them into a different type of node and assign specific measurements and thresholds to them.

## Fleet Tracking

Imagine you own a fleet of trucks. Virtual nodes are a perfect way to manage your fleet's inventory. Every truck within your fleet can be tracked and managed in the same within a few minutes. As your fleet changes, it's as simple as updating a spreadsheet and re-importing the data on the parent node.
