---
title: "Agent Reports Multiple Values"
date: 2024-02-08T09:26:39-08:00
draft: false
---

# Report Multiple Values

To have your agent report multiple values, please do the following:

```json
{
    "parent": {"property": "path", "value": "com.example.seattle"},
    "type": "machine",
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "weltall-0092", "monitor_name": "Stats"},
    "values": [
        {"name": "cpu", "value": 0.6, "threshold": {"above": 0.95, "level": "critical"}},
        {"name": "ram", "value": 0.7, "threshold": {"above": 0.8, "level": "warning"}},
        {"name": "hdd", "value": 0.2, "threshold": {"above": 0.75, "level": "error"}}
    ]
}
```

This will report three different values for `cpu`, `ram`, and `hdd` resource utilization. If any one of these values breach their respective threshold, the monitor will transition into the respective configured `level`.

In this context, **@ys** will create four monitors on this node.

- An elder monitor named `Stats`
- A sibling monitor named `cpu`
- A sibling monitor named `ram`
- A sibling monitor named `hdd`

## More reading

- [Available Agent Threshold Types]({{< relref "library/agents-threshold-types.md" >}})
