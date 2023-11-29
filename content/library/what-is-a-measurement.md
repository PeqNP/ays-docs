---
title: "What Is a Measurement?"
date: 2022-05-17T08:54:49-07:00
draft: false
---

# Monitors

A monitor is the combination of a sensor (data source) and threshold configuration.

## Sensor

A sensor can be

1. a script that is executed at a configured interval (i.e. every 1 minute)
1. a service that sends data points directly to **@ys**

The most common sensor type is a (Python) script that queries an external data source such as New Relic, Datadog, etc. Each time the script runs, **@ys** will query the data source and log the return value.

## Threshold Configuration

A threshold configuration defines the "health" (nominal state) of a monitor. The nominal state is any value between a min and/or max range. If the data points logged from the sensor are inside the min or max range, a monitor is considered "healthy." If the data points logged fall outside of the min or max range, the monitor will be considered "unhealthy."

You can also configure a monitor's alerting level. The alerting levels are `Warning`, `Error`, and `Critical`. Each alerting level has their own "weight". The greater the "weight", the more it will affect the health of a Node.

For example, if a data point breaches a `Warning` threshold, then the monitor will be considered in a `Warning` state. This `Warning` state may place the monitor's node in a `Warning` health state.

### Types of Thresholds

- `Above` (>) - A value that is above this range will trigger an alert
- `Below` (<) - A value that falls below this range will trigger an alert
- `Boundary` (< `min`, > `max`) - Any value that falls outside of the `min` / `max` range will trigger an alert
- `Equal` (=) - Any value that is equal to this threshold will trigger an alert
- `Not Equal` (!=) - The inverse of `Equal`, where any value that does _not_ equal the threshold will trigger an alert

## Types of Monitors

- Normal: Allows owner of monitor to configure every property of the monitor.
- Template: Allows owner of monitor to configure most properties of the monitor, including thresholds, etc.
- Reference: A monitor that references another monitor's configuration. These monitors are read-only.

## More Reading

- [How do I configure a monitor sensor?]({{< relref "library/how-do-i-configure-a-measurement-sensor.md" >}})
- [How is node health determined?]({{< relref "library/how-is-node-health-determined.md" >}})
- [How do I modify a reference monitor?]({{< relref "library/how-do-i-modify-a-reference-measurement.md" >}})
- [How to understand monitor health]({{< relref "library/how-to-understand-measurement-health.md" >}})

