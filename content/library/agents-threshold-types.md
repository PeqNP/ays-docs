---
title: "Agent Threshold Types"
date: 2024-02-08T09:26:58-08:00
draft: false
---

# Agent Value Threshold Types

A threshold is an optional value that allows you to configure the error state of a monitor. If the respective sample value breaches the threshold configuration, the threshold will transition the monitor to the respective alerting level.

Thresholds can be configured on the status `value` or status `values` property.

## `above` Threshold

If a value goes `above` this threshold, the threshold will be breached:

```json
    {"name": "cpu", "value": 0.6, "threshold": {"above": 0.95, "level": "critical"}},
```

If `value`, `0.6`, goes `above` `0.95`, the monitor will transitino into a `critical` state.

## Alerting Levels

The available alerting levels are `warning`, `error`, and `critical`. Each level represents a different "health" value. `warning` is considered 30% unhealthy, `error` 60% unhealthy, and `critical` 100% unhealthy. This "health" value effects how the health is reported within the app but also how it affects the health of related nodes. For more information, please refer to [How is Node Health Computed?]({{< relref "library/how-is-node-health-computed.md" >}}).
