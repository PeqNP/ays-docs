---
title: "Agent Parent Relationship"
date: 2024-02-08T08:36:10-08:00
draft: false
---

# Associate Agent to Pre-Existing Parent Node

The following example will associate your agent monitor to a pre-exising parent node as a new monitor.

```json
{
    "parent": {"property": "path", "value": "com.example.mobile.ios"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "parent", "monitor_name": "Max Requests Breached on Product Service"}
}
```

This will associate your agent as a new monitor, called `Max Requests Breached On Product Service` to the `com.example.mobile.ios` node.

Now we need to track the health of the monitor. How would you like to do that?

- [Provide a single value with a threshold]({{< relref "library/agents-single-value.md" >}})
- [Provide multiple values with a threshold]({{< relref "library/agents-multiple-values.md" >}})
- [Provide a health status]({{< relref "library/agents-status-value.md" >}})
