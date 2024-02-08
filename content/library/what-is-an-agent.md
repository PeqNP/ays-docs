---
title: "Self Reporting Agents"
date: 2024-02-08T07:46:04-08:00
draft: false
---

# Self Reporting Agents

Agents allow any system to self-report its status. Some common examples of possible agents:

- IoT devices
- 3rd party webhooks, such as a NewRelic alert webhook
- Services that may be brought up or down depending on demand

An agent can relate to a pre-configured node in the system, or it can create its own node as a child to a parent node. An agent may also template another node. This makes it simple to configure any sized group of nodes to behave in the same way.

If you know what you need, please visit the API docs for the `/agent/` endpoint at the [External Services Documentation](https://api.bithead.io:9443/docs) page.

## Examples

You can jump right in with these examples. What are you trying to do?

- [Create a new agent monitor on a pre-existing parent node](({{< relref "library/agents-relationship-parent.md" >}}))
  - Useful to track, and group, multiple different types of system issues from 3rd party analytics providers (refer to `Report uptime status`)
- [Create a new child node that lives under the parent node]({{< relref "library/agents-relationship-child.md" >}})
  - IoT devices
  - Scalable systems that are built up / torn down depending on need
- [Report a single value]({{< relref "library/agents-single-value.md" >}}), creating a single monitor
  - IoT sensors that report a single value (humidity, water level, light level, etc.)
- [Report multiple values]({{< relref "library/agents-multiple-values.md" >}}), creating multiple monitors for each value
  - Proxies that report number of requests, number of errors, etc.
  - Machine status such as CPU, HDD, RAM, and network utilization
- [Report uptime status]({{< relref "library/agents-status-value.md" >}}), create a monitor that represents the uptime status of a system
  - Integrate a 3rd party provider which reports the status of your system(s) via a webhook. The system may trigger an unhealthy state and may also (optionally) recover from an unhealthy state.
- [Template a pre-configured node]({{< relref "library/agents-template.md" >}}) to adopt monitor configuration
  - A group of systems must behave in the same way

## Required Configuration

Every agent must provide the following:

- The parent the agent is associated to
- An "org secret" to ensure you have access to add nodes to the organization. Ask your admin for this value.
- How the agent relates to the parent (more on this later)

### Relationships

An agent may relate:

- Directly to a parent node as a new monitor. This is ideal when you want to group many (3rd party) services together on a single node.
- As a child to the parent. This is ideal for grouping IoT devices, machines, and possibly services by a physical region, building, or floor.

A special type of relationship exists which allows more than one agent to relate to the same child node as different monitors. Please refer to the child relationship documentation for more information.

How you group nodes is up to you. **ays** gives you the power to manage your hierarchy in the way that best suits your needs.

I want to create a:

- [Parent relationship]({{< relref "library/agents-relationship-parent.md" >}})
- [Child relationship]({{< relref "library/agents-relationship-child.md" >}})

### Values & Statuses

There are four ways to send status to **ays** from your agent.

- Provide a single value. e.g. A sensor value for humidity, light, or water level
- Provide multiple values. e.g. If monitoring a server, you may provide CPU, HDD, RAM, and Network in the same status payload.
- Provide a health status. e.g. 3rd party analytics provider, such as NewRelic, can send a signal (via a webhook) that a threshold was breached. It can also send the recovery signal.
- No value or status. When coupled with heartbeat configuration, this helps you know if the system is online. Obviously, this doesn't provide any additional insight into the state of the system.

I want to configure an agent to report:

- [Single value]({{< relref "library/agents-single-value.md" >}})
- [Multiple values]({{< relref "library/agents-multiple-values.md" >}})
- [Health Status]({{< relref "library/agents-status-value.md" >}})
- Nothing. Simply omit any value or status from the payload.

### Heartbeat

The heartbeat configuration allows you to configure your agent to alert if no signal has been received from the agent within a given timeout.

- [Configure Agent Heartbeat]({{< relref "library/agents-heartbeat.md" >}})

### Properties

Properties are an important way to track state information on an agent. For example, an IoT device may report its IP address, firmware version, or any other configuration as a node property.

Properties may also be used by the Node API to target agent systems. For example, if the IP address of an IoT is provided, the Node API may send a request to that device to update its firmware.

- [Add Node Properties]({{< relref "library/agents-node-properties.md" >}})

### Templates

There may be times when you need a group of systems to behave in the same way. Templates allow you to do this by pre-configuring alerting and monitors that an agent system will adopt.

- [Adopt a Template]({{< relref "library/agents-template.md" >}})
