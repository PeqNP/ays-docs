---
title: "How Do I Configure New Relic"
date: 2022-09-21T10:51:53-07:00
draft: false
---

# How Do I Configure New Relic?

Configuring New Relic requires three flows:
- Associating the New Relic Entity GUID to an **@ys** Node
- Creating a New Relic webhook that sends alerts to the **@ys** webhook service
- Configuring policies to send condition alerts to the **@ys** webhook

## Associating New Relic Entity GUID to **@ys** Node

Sign in to your [New Relic](https://www.newrelic.com) account.

Go to "All Entities."

On the entity you wish to track, such as an iOS app, tap the ellipses button at the right-most of the cell.
Tap the "See metadata & tags" option.

![New Relic Metadata](/help/img/new-relic-metadata.png)

Copy the "Entity guid."

![New Relic Entity GUID](/help/img/new-relic-entity-guid.png)

Navigate to the respective Node in **@ys** you wish to configure the app to in **@ys**.

Tap on "External alerting".

Paste the entity guid value into the "Entity GUID" field under the "New Relic" group.

![New Relic External Config](/help/img/new-relic-external-config.png)

Go back to the previous page and "Save" the node.

## Configuring a New Relic Webhook

While still signed in, tap the "Alerts & AI" tab on the left.

Tap on "Destinations."

Tap on "Webhook."

![New Relic External Config](/help/img/new-relic-destinations.png)

You will see the "Add a destination" group with two fields.

- Enter `@ys` for the "Webhook name"
- Enter `https://api.getbithead.com:9443/newrelic` for the "Endpoint URL"
- Save the destination (button on the bottom right)

![New Relic External Config](/help/img/new-relic-webhook.png)

**Please note:** The Webhook URL may be different for you if you are self hosting **@ys**!

The Endpoint URL will be available within the **@ys** app in the future. For now, please contact your system administrator for this URL.

## Configure Policy Webhook

**@ys** accepts alerts from the modern New Relic alerting system called a "Workflow." A workflow can include alerting configuration for one or more policies. A policy consists of one or more "Conditions." This one to many relationship between "conditions" and a "policy" reduces the number of locations you need to configure your webhook.

All this to say, that you must have configured your alerting to use workflows. And, you may only need to update a single policy workflow to capture all signals from every condition.

To configure a workflow, do the following:

Tap on "Alerts & AI."

Tap on "Workflows."

Tap on the policy to configure.

![New Relic Policies](/help/img/new-relic-policies.png)

Scroll down to the "Notify" group and tap the "Webhook" button.

![New Relic Policies](/help/img/new-relic-policy-add-webhook.png)

This will show the "Edit notification message" form.

Select `@ys` as the "Destination."

Paste the following template into the "Payload template" field

```
{
    "parent": {"property": "path", "value": "com.example.mobile.ios"},
    "org_secret": "your_org_secret_goes_here",
    "relationship": {"type": "parent", "monitor_name": {{ json annotations.title.[0] }} },
    "status": {
        "message": {{ json annotations.title.[0] }},
        "state": "{{ eq priority "CRITICAL" yes='critical' no='error' }}"
    }
}
```

This will associate all NewRelic alerts, as new monitors, to the `com.example.mobile.ios` parent node. Please refer to the [Agent Sensor docs]({{< relref "library/what-is-an-agent.md" >}}) for more information on how to associate agent alerts as new child nodes, etc.

**Please note:**
- This will consider any message sent from NewRelic as critical or error status. This means, even if the error comes out of a bad state, it will not self heal. These docs will be updated with a better configuration once I discover a better way to format the `state` value, given their toolset.
- Please refer to [NewRelic Docs](https://docs.newrelic.com/docs/alerts-applied-intelligence/notifications/message-templates/#json) when determining which fields to use for your alerts. You may wish to include a condition, issue information, etc. to the alert.

Tap the Save / Update message button

![New Relic Policies](/help/img/new-relic-policy-webhook-config.png)

Please tap the "Test workflow" to ensure integration is complete.

Please do this for every other policy workflow that needs to send data to **@ys**.
