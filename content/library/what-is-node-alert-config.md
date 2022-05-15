---
title: "What Is Node Alerting Configiguration?"
date: 2022-05-15T06:54:27-07:00
draft: false
---

# Node Alerting Configuration

Alerting configuration works like a typical logging system where you can filter what messages are logged depending on the configured "level". For example, in production you may configure your logging level to "Error." Any logs emitted at a lower logging level than "Error" (Debug, Info, Warning) will not be emitted.

This form provides a way to configure this "logging level." `Actions` configured to the respective group (Children, Dependencies, and Measurements) will not trigger unless the respective threshold level has been breached.

For example, imagine you configure a node's `Dependencies` threshold value to `Warning` and configure a Slack action to trigger when the threshold is breached. If a node's dependencies health breach the `Warning` threshold, a message will be sent to Slack.

If you configure a node's `Dependencies` threshold value to `Error`, and a dependency's health breaches a `Warning` threshold, no message will be sent to Slack as `Warning` is lower than the `Error` level.

There are currently three groups that you can configure `Children`, `Dependencies`, and `Measurements`. Using the same logic above, as described with `Dependencies`, if any of the node's children breach a configured threshold level, then the actions will trigger. The same with `Measurements`.

## Measurements

Currently measurements allow you to configure actions when a threshold is breached. This alerting configuration does **not** overwrite any configuration associated to a Measurement. Therefore, you will always get alerts configured on the measurement in **all** cases. To be clear, turning Measurements `Off`, when a measurement has its own threshold configuration, will _not_ disable these alerts from triggering. If you wish to have a single location where you configure alerting **do not assign `Actions` to thresholds on the respective Measurements.**


`Deprecatation Warning`

Measurement alerting configuration is deprecated and may be removed in the future.
