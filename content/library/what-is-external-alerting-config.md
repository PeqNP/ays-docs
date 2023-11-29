---
title: "What Is External Alerting Config"
date: 2022-09-21T10:40:11-07:00
draft: false
---

# What is External Alerting Config?

An external system, such as Embrace and NewRelic, may be configured to send alerts to **@ys**.

This is the easiest and fastest way to determine the health of your systems if you have already configured your apps, services, etc. with an external alerting system.

External alerting configuration are treated as "virtual monitors." In other words, an external alert (e.g. a "Condition" in NewRelic or an "Alert" in Embrace) is similar to an **@ys** monitor.

When an external system sends an alert for a specific condition / alert, **@ys** will translate the alerting level and update the health of the node. The health of the node can be "cured" manually by a user or automatically if the external system detects a recovery. Please note that some sytems may not send a "recovery" event. In these cases an **@ys** user must be responsible for manually curing the event from the Node's form.

# Configure External Alerting Systems

- [How do I Configure Embrace?]({{< relref "library/how-do-i-configure-embrace.md" >}})
- [How do I Configure New Relic?]({{< relref "library/how-do-i-configure-new-relic.md" >}})
