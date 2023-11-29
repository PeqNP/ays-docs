---
title: "Read-only Threshold"
date: 2022-03-07T05:21:09-08:00
draft: false
---

# Read-only Threshold

When a Threshold is set as "read-only", all other nodes that template from this monitor will be unable to change the configuration values of threshold actions.

Imagine you have a group of services which must send all alerting traffic to a specific Slack channel. You would turn on "read-only" in this context. In essence, this creates a central configuration point for your alerting configuration.

If you are creating a monitor template which will be used by many teams within (or outside) of your organization, the configuration values will most likely be different per team. In this context, you would turn "read-only" off. `com.bithead.template.ping` is an example of a read-only threshold. `ping` is designed to be used by all organizations. Therefore, the Slack channel alerting configuration can be modified to use the respective team's channel.

If you are not sure which option to choose, keep "read-only" on.
