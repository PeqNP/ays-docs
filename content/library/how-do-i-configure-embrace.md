---
title: "How Do I Configure Embrace"
date: 2022-09-21T10:51:45-07:00
draft: false
---

This configuration is currently out-of-date. **@ys** does not currently support Embrace.

# How Do I Configure Embrace?

Configuring Embrace requires three flows:
- Associating the Embrace App ID to an **@ys** Node
- Creating an Embrace webhook that sends alerts to the **@ys** webhook service
- Configuring alerts to send to the **@ys** webhook

## Associate Embrace App ID to an **@ys** Node

Sign in to your [Embrace](https://embrace.io) account.

Tap on the "(Switch) App" icon (currently the top-most button in the left tab bar on desktop). You should see a list of your apps that you are monitoring.

Tap on the the "API Key" button for the app you wish to configure in **@ys**.

![Embrace App API Key](/help/img/embrace-app.png)

This should bring you into the app's settings with the "App" tab selected (first tab on top left of page).

Scroll down and find your app's ID. Copy the value in this field.

![Embrace App API](/help/img/embrace-app-id.png)

Navigate to the respective Node in **@ys** you wish to configure the app to in **@ys**.

Tap on "External alerting".

Enter in the app ID value into the "App ID" field under the "Embrace" group.

![Embrace External Config](/help/img/embrace-external-config.png)

Go back to the previous page and "Save" the node.

## Configuring the Embrace Webhook

This assumes you are still in the respective Embrace app "Settings" page.

Tap on the "Notifications" tab.

You will see the "Webhook Integration" group with two fields.

- Enter `@ys` for the "Nickname"
- Enter `https://api.getbithead.com:9443/embraceio` for the "Webhook URL"
- Save the webhook

![Embrace Webhook Config](/help/img/embrace-webhook-config.png)

Please feel free to test the integration by tapping the "Test" button.

**Please note:** The Webhook URL may be different for you if you are self hosting **@ys**!

The Webhook URL will be available within the **@ys** app in the future. For now, please contact your system administrator for this URL.

## Configuring Alerts

You should have successfully configured your app to an **@ys** Node and have tested to make sure it works. Now it's time to send alerts to **@ys**.

Tap on the "Alerts" tab (currently bottom-left on left tab bar on desktop).

Tap on the "Edit" (pencil icon) for the alert you wish to send to **@ys**.

Scroll down to the "Send to Webhooks" group.

Tap the "Send to webhooks" option and select the `@ys` webhook.

![Embrace Alert Config](/help/img/embrace-alert-config.png)

Please do this for every other alert you wish to send to **@ys**.
