---
title: "Adopt an Agent Template"
date: 2024-02-08T09:28:27-08:00
draft: false
---

# Adopt an Agent Template

It may be necessary to manage a group of systems to behave in the same way. Templates allow you to do this by pre-configuring alerting and monitoring that an agent can adopt.

Below is an example of an agent adopting a template with an elder monitor.

```json
{
    "parent": {"property": "path", "value": "com.example.iot"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", path: "bed-42", "monitor_name": "Grow Bed"},
    "template": "com.example.template.grow-bed",
    "values": [
        {"name": "water", "value": 0.3},
        {"name": "light", "value": 1200},
        {"name": "humidity", "value": 0.2}
    ]
}
```

This will create a `water-sensor` node. It will _adopt_ the template `com.example.template.grow-bed`. Including its elder monitor `Grow Bed` and its three sibling monitors `water`, `light`, and `humidity`. In other words, the `Grow Bed`, `water`, `light`, and `humidity` monitors are _pre-configured_ on the template node within **@ys**. In order for an agent to adopt a template, _every monitor name must match every template's monitor name_.

Please note that the `values` _do not_ have threshold configuration! This configuration lives on the template.

The following configuration is ignored and will be configured on the template within **@ys**:

- Value threshold configuration
- Heartbeat configuration

You can just as easily adopt a template that reports a single value or a status. However, the same rule applies for all template types; every agent monitor name must match with every template monitor name. Failing to do this will raise an exception.
