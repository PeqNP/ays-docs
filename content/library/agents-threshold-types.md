---
title: "Agent Threshold Types"
date: 2024-02-08T09:26:58-08:00
draft: false
---

# Agent Value Threshold Types

A threshold is an optional value that allows you to configure the error state of a monitor. If the respective sample value breaches the threshold configuration, the threshold will transition the monitor to the respective alerting level.

Thresholds are configured on the status `value` or `values` property.

## `above` Threshold

If a value goes `above` the threshold, the threshold will be breached:

```json
{"name": "cpu", "value": 0.6, "threshold": {"above": 0.95, "level": "critical"}},
```

If `value`, `0.6`, goes `above` `0.95`, the monitor will transition into a `critical` state.

## `below` Threshold

If a value goes `below` the threshold, the threshold will be breached:

```json
{"name": "cpu", "value": 0.6, "threshold": {"below": 0.95, "level": "error"}},
```

If `value`, `0.6`, goes `below` `0.95`, the monitor will transition into a `error` state.

## `equal` Threshold

If a value is `equal` the threshold, the threshold will be breached:

```json
{"name": "cpu", "value": 0.6, "threshold": {"equal": 0.95, "level": "warning"}},
```

If `value`, `0.6`, is `equal` to `0.95`, the monitor will transition into a `warning` state.

## `nequal` Threshold

If a value is **not equal** to the threshold, the threshold will be breached:

```json
{"name": "cpu", "value": 0.6, "threshold": {"nequal": 0.95, "level": "warning"}},
```

If `value`, `0.6`, is **not equal** to `0.95`, the monitor will transition into a `warning` state.

## `outside` Threshold

If a value is `outside` the threshold range, the threshold will be breached:

```json
{"name": "cpu", "value": 0.6, "threshold": {"outside": {"min": 0.20, "max": 0.95} "level": "critical"}},
```

If `value`, `0.6`, is `outside` the range of `0.20` and `0.95`, the monitor will transition into a `critical` state.

## Alerting Levels

The available alerting levels are `warning`, `error`, and `critical`. Each level represents a different "health" value. `warning` is considered 30% unhealthy, `error` 60% unhealthy, and `critical` 100% unhealthy. This "health" value effects how the health is reported within the app but also how it affects the health of related nodes. For more information, please refer to [How is Node Health Computed?]({{< relref "library/how-is-node-health-computed.md" >}}).
