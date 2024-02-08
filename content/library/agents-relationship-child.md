---
title: "Agent Child Relationship"
date: 2024-02-08T08:44:41-08:00
draft: false
---

# Associate Agent as Child Node to Parent Node

The following example will create a new node that is associated to a parent node. This will also create the monitors required to report the status of your agent.

```json
{
    "parent": {"property": "path", "value": "com.example.seattle"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "weltall-0092", "monitor_name": "Statistics"}
}
```

This will create a new child node, `weltall-0092`, to the `com.example.seattle` parent. The full path to your agent will be `com.example.seattle.weltall-0092`. A monitor called `Statistics` will be created. The monitor will presumably provide machine stats.

**@ys** also allows you to group child nodes in a more granular way. For example, you can tell **@ys** to auto-create parent nodes that better define your machine's location. Here's an example:

```json
{
    "parent": {"property": "path", "value": "com.example.seattle"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "colocation-1.floor-3.quadrant-1.weltall-0092", "monitor_name": "Statistics"}
}
```

The `path` property represents a _relative_ path to the parent. The full path of this node will be `com.example.seattle.colocation-1.floor-3.quadrant-1.weltall-0092`. Again, **@ys** will _automatically_ create all parent nodes for you. This is extremely useful when you need a way to logically group 100s or 1000s devices within a given group. It also allows you to write Node APIs that can target specific system groups to update.

Agents may also be grouped within the same child node. This is useful when you have multiple systems (e.g. sensors) that report a single value but must be represented as a single node. Imagine you have two sensors. One tracks humidity and the other the water level. Each sensor will send its own messsage.

**Humidity Sensor**

```json
{
    "parent": {"property": "path", "value": "com.example.idaho"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "building-1.room-4.quadrant-2.bed-42", "monitor_name": "Humidity"},
    "managed": false
}
```

**Water Level Sensor**

```json
{
    "parent": {"property": "path", "value": "com.example.idaho"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "building-1.room-4.quadrant-2.bed-6", "monitor_name": "Water Level"},
    "managed": false
}
```

Both of these sensors will be associated to the same `bed-6` node as different monitors, `Humidity` and `Water Level`, respectively.

You _must_ set the `managed` property to `false`. This ensures each sensor's configuration won't over-write the other's. Failing to do this will result in each sensor removing the other monitor from the node each time they self-report. Essentially, when an agent is _unmanaged_ it allows multiple agent  monitors to live side-by-side.

**NOTE:** The `managed` property is available only when the relationship type is `child`.

Now we need to track the health of the monitor. How would you like to do that?

- [Provide a single value with a threshold]({{< relref "library/agents-single-value.md" >}})
- [Provide multiple values with a threshold]({{< relref "library/agents-multiple-values.md" >}})
- [Provide a health status]({{< relref "library/agents-status-value.md" >}})
