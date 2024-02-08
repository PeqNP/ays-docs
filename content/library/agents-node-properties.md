---
title: "Agent Node Properties"
date: 2024-02-08T09:28:14-08:00
draft: false
---

# Add Node Properties From Agents

An agent may self report properties about its internal state to **@ys**.

Some common properties to track:

- Name of machine (if different from node name)
- IP address
- Firmware version (IoT)
- etc.

You may report any value that may be useful.

Properties can also be used to target systems using the [Node API]({{< relref "library/what-is-a-node-api.md" >}}).

To send properties from an agent, please do the following:

```json
{
    "parent": {"property": "path", "value": "com.example.seattle"},
    "type": "machine",
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", "path": "weltall-0092", "monitor_name": "Stats"},
    "properties": [
        {"name": "ip_address", "value": "192.168.0.1"},
        {"name": "firmware_version", "value": "1.0.23 b64"}
    ]
}
```

This will create two properties `ip_address` and `firmware_version`.

## Notes

- Properties are removed if the agent is `managed` and the property no longer exists in the agent message.
- You can view these properties on the node either through the Node Form or the Node Tactile Form.
- Node properties are not required to look like variable names. The naming convention used at Bithead is to use Python variable names to keep naming consistent and to help aid writing Node APIs.
