---
title: "How Do I Configure New Relic"
date: 2022-09-21T10:51:53-07:00
draft: false
---

# How Do I Configure New Relic?

Configuring New Relic requires:

- Creating a New Relic webhook that sends alerts to the **@ys** [agent service]({{< relref "library/what-is-an-agent.md" >}})
- Configure policies to send condition alerts to the **@ys** agent service

## Configure a New Relic Webhook

- Sign in to your account
- Tap the `Alerts & AI` tab on the left
- Tap on `Destinations`
- Tap on `Webhook`

![New Relic External Config](/help/img/new-relic-destinations.png)

You will see the "Add a destination" group with two fields.

- Enter "@ys" for the `Webhook name`
- Enter `https://api.bithead.io:9443/agent` for the `Endpoint URL`
- Save the destination (button on the bottom right)

![New Relic External Config](/help/img/new-relic-webhook.png)

**Please note:** The Webhook URL may be different for you if you are self hosting **@ys**!

The Endpoint URL will be available within the **@ys** app in the future. For now, please contact your system administrator for this URL.

## Configure Policy Webhook

**@ys** accepts alerts from the modern New Relic alerting system called a "Workflow." A workflow can include alerting configuration for one or more policies. A policy consists of one or more "Conditions." This one to many relationship between "conditions" and a "policy" reduces the number of locations you need to configure your webhook.

All this to say, that you must have configured your alerting to use workflows. And, you may only need to update a single policy workflow to capture all signals from every condition.

To configure a workflow, do the following:

- Tap on `Alerts & AI`
- Tap on `Workflows`
- Tap on the policy to configure

![New Relic Policies](/help/img/new-relic-policies.png)

Scroll down to the `Notify` group and tap the `Webhook` button.

![New Relic Policies](/help/img/new-relic-policy-add-webhook.png)

This will show the "Edit notification message" form.

Select `@ys` as the `Destination`.

Paste the following template into the `Payload template` field

```
{
    "parent": {"property": "path", "value": "com.example.mobile.ios"},
    "org_secret": "your_org_secret_goes_here",
    "relationship": {"type": "parent", "monitor_name": {{ json annotations.title.[0] }} },
    "status": {
        "message": {{ json annotations.title.[0] }},
        "state": "{{#if (eq state "CLOSED")}}healthy{{else}}{{#eq priority "CRITICAL"}}critical{{else}}{{/eq}}{{#eq priority "ERROR"}}error{{else}}{{/eq}}{{#eq priority "WARNING"}}warning{{else}}{{/eq}}{{#eq priority "LOW"}}warning{{else}}{{/eq}}{{/if}}"
    }
}
```

This will associate all NewRelic alerts, as new monitors, to the `com.example.mobile.ios` node. Please enter the correct node path you wish to associate these alerts to. For more information on how to associate agent alerts as new child nodes, please refer to the [Agent Sensor docs]({{< relref "library/what-is-an-agent.md" >}}).

Please refer to the [NewRelic Docs](https://docs.newrelic.com/docs/alerts-applied-intelligence/notifications/message-templates/#json) when determining which fields to use for your alerts. You may wish to include a condition, issue information, etc. to the alert.

Tap the Save / Update message button

![New Relic Policies](/help/img/new-relic-policy-webhook-config.png)

Please tap the `Test workflow` button to ensure integration works successfully.

Please do this for every other policy workflow that needs to send data to **@ys**.
