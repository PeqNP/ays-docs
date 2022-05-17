---
title: "What Is Node Alerting Configuration?"
date: 2022-05-15T06:54:27-07:00
draft: false
---

# Node Alerting Configuration

Alerting configuration works like a typical logging system where you can filter what messages are logged depending on the configured "level." For example, in production you may configure your logging level to "Error." Any logs emitted at a logging level lower than "Error" (Debug, Info, Warning) will not be emitted.

This form provides a way to configure this "logging level." `Actions` configured to the relationship type (Children, Dependencies, and Measurements) will trigger if their health level breaches the respective `Warning`, `Error`, or `Critical` level.

For example, imagine you configure a node's `Dependencies` threshold value to `Warning` and configure a single Slack action. If any of the node's dependencies health breach the `Warning` threshold, a message will be sent to Slack.

If you configure a node's `Dependencies` threshold value to `Error`, and a dependency's health breaches a `Warning` threshold, no message will be sent to Slack as `Warning` is a lower level than `Error`.

Please refer to [What is a Node Relationship?]({{< relref "library/what-is-a-node-relationship.md" >}}) to get more information on how the health of `Children` and `Dependencies` are determined.

## `Children`

Children refer to any nodes that are a child to the respective node. Therefore, if any child has a health that breaches a configured level, the respective actions will be triggered.

## `Dependencies`

Dependencies refer to any node that this subject node depends on. If any dependency breaches a configured level, the respective actions will be triggered.

## `Measurements`

Please refer to [What is a Measurement?]({{< relref "library/what-is-a-measurement.me" >}}) for more context.

The alerting configuration at the node level will **not** overwrite the behavior of actions configured to a measurement. Therefore, actions configured on a measurement will be triggered _in addition_ to any actions you configure at the node level. However, turning the node configuration for measurements `Off`, will prevent actions on the measurements from being triggered.

If you wish to have a single location where you configure alerting actions **do not assign `Actions` to thresholds on the respective measurements.** This is especially true for templates. Allow the consumer of the template to configure the actions on template measurements via the node configuration.

`Deprecatation Warning`

Measurement alerting configuration is deprecated and may be removed in the future.
