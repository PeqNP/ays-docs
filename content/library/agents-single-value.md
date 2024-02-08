---
title: "Agent Reports Single Value"
date: 2024-02-08T09:01:47-08:00
draft: false
---

# Report a Single Value

To have your agent report a single value, please do the following:

```json
{
    "parent": {"property": "path", "value": "com.example.seattle"},
    "type": "machine",
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "weltall-0092", "monitor_name": "CPU"},
    "value": {"name": "cpu", "value": 0.5, "threshold": {"above": 0.95, "level": "critical"}}
}
```

This will report a single value that represents the load of the `cpu`. If the `value` (in this context `0.5`) goes `above` the threshold of `0.95`, the monitor will be transition into a `critical` state.

- [Available Agent Threshold Types]({{< relref "library/agents-threshold-types.md" >}})
