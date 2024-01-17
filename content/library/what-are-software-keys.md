---
title: "What Are Software Keys"
date: 2024-01-09T16:53:34-08:00
draft: false
---

# What are Software Keys?

Many services, machines, etc. may require credentials in order to access the resource. For example, if you wish to query a NewRelic REST API, you must provide an API API key.

## Types of Software Keys

There are two types of software keys:

- Node keys
- Global keys

**Node keys** are software keys associated to a node. Software keys _may_ be inherited so that children can access a parent's keys. This is useful when you need to share a software key across many teams.

Software key values are _not_ shown to users witin the **@ys** app or even transferred over the wire. Only the first six characters of the key are shown to help distinguish between keys. This may be changed in the future to hide the key entirely.

**Global keys** are keys that can be accessed across organizations. Global keys are required for some template nodes. For example, Bithead has a template node to query information from NewRelic called, `com.bithead.template.new-relic`. In order to query NewRelic, the template needs your NewRelic API key. A global key in the system exists called `NewRelic API Key`. Imagine you have a node, `com.example.mobile.ios` which templates from `com.bithead.template.new-relic`. Your `ios` node would configure the `NewRelic API Key` within its software keys configuration. Once that is finished, the template monitor will have access to the API key.

If a global key is required, but not configured, you will see an error message in the monitor graph.

## Important Notes

### Encryption

Software keys are _not_ encrypted. If they are hashed, there is no way to decrypt and provide the respective key to the external resource. There are plans to use PBES2 (Password Based Encryption Scheme 2) or SQLCipher in the near future. We do not recommend storing credentials to critical servers in **@ys**.

Possible work-arounds:
- Use a JWT that represents a signed in user. Rotate the keys as necessary.
- If hosting your own instance of **@ys**, from a secure network, you may access resources directly.
- Push data directly to **@ys**. There are plans to create an agent that will send data directly to **@ys**. If you need this feature now, please contact us.

We recommend to provide software keys that you would otherwise feel comfortable adding to a mobile application. In this respect, **@ys** is more secure as the user does not have access to the source code to reverse engineer the key.

### Backups

Software keys are stored directly on the **@ys** system. There are no middleware services. This was done to mitigate vectors of attack. If you are hosting your own instance of **@ys** you may choose to `scp` the database to another, secure, server.
