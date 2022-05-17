---
title: "What Is a Measurement?"
date: 2022-05-17T08:54:49-07:00
draft: false
---

# Measurements

A measurement is the combination of a data source and threshold configuration.

## Data Source

A data source can be

1. a script that is executed at a configured interval (i.e. every 1 minute)
1. a service that sends data points directly to @ys

The most common data source is a (Python) script that queries an external data source such as New Relic, Datadog, etc. Each the time the script runs, the data point derived from the external source is saved to the database.

## Threshold Configuration

A threshold configuration defines the nominal state of a Measurement from a collected data point or a set of collected data points over time. More simply, it defines what it means for a measurement to be "healthy." The threshold's minimum and maximum values define if the data points represent a "healthy", `Warning`, `Error`, or `Critical` state.

For example, if a data point breaches a `Warning` threshold, then the measurement will be considered in a `Warning` state. This state is used to determine the health of the node that the measurement is associated to. A node's "health" value also propagates to its dependents and parents. Rather, if this node (which will we refer to as node "A") is a dependency to node "B", then node B's health may be affected by node A's health by virtue of it being dependent on node A.

```
Measurement with `Warning` state -> affects Node A health -> affects Node B health (dependent on A)
```
