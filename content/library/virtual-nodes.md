---
title: "Virtual Nodes"
date: 2022-03-13T22:06:59-07:00
draft: false
---

# Virtual Nodes

Virtual nodes are read-only nodes which inherit all properties from a template node. They may only be created, updated, or deleted from their parent node.

Virtual modes can be considered as ephemeral, although their life span depends on the context.

The typical use case for virtual nodes is that you wish to quickly assign the same monitors to many nodes. In other words, they represent an asset or service that share the same properties.

## Micro services

Imagine you have a micro service which can scale from 1 to N instances. Each instance must be managed the same way. At your service provides a public API that you can use to update the number of services in real-time. Now you can see the number of instances, and track the status of each micro service within the **At Your Service** app.

## Mobile app

Your company's mobile app consumes more than 30 external services. You need a way to track each of these 30 services in the same way. For instance, you may wish to track latency, requests per second, error rate, etc. Create a template node that measures each data point, and assign your virtual nodes to this template. Now you can the see the health of every service you depend on within the **At Your Service** app.

If one of the services require more finely tuned monitors (alerting threshold, sample interval, etc.), you may convert the node to a different type allowing you to make changes to it.

## Fleet Tracking

Imagine you own a fleet of trucks. Every truck within your fleet must be tracked and managed in the same way. For example, you may wish to track fuel consumption, idle time, etc. Virtual nodes provide a way to import your entire fleet, via a spreadsheet, in one simple step. As your fleet changes, it's as simple as updating the spreadsheet and re-importing the data.
