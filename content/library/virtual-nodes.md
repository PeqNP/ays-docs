---
title: "Virtual Nodes"
date: 2022-03-13T22:06:59-07:00
draft: false
---

# Virtual Nodes

Virtual nodes are read-only nodes which inherit all properties from a template node. They may only be created, updated, or deleted from their parent node.

Virtual nodes can be considered as ephemeral, although their life span depends on the context.

The status of every virtual node is queried at _the same time_.

The typical use case for virtual nodes is quickly assign the same monitor(s), to many nodes, and query the status of each node using a single query.

## Use Cases

### Status availability

A service you depend on, such as Atlassian, provides a public status page which includes every service and its respective status. To monitor this resource, you would request the URL, parse the page's contents, and then transform each service and status into a virtual node.

### Micro services

Imagine you have a micro service which can scale from 1 to N instances. Each instance's resources must be tracked the same way. For example, the CPU, RAM, and disk usage.

This can be accomplished with the combination of a template node and virtual nodes. The primary monitor on your template node will query a server for the list of microservice instances along with status. Then, add monitors on the template node that represent the CPU, RAM, and disk usage. The data queried from the primary monitor will then filtered to the respective monitors for each instance.

### Fleet Management

Imagine you own a fleet of trucks. Every truck within your fleet must be tracked and managed the same way. For example, you may wish to track fuel consumption, idle time, etc. This can be accomplished by querying a database that contains your fleet along with the respective status of each truck. As your fleet changes, update the database and **At Your Service** will automatically add and remove the assets that are tracked.

## Example Scripts

Using our Status availability use case, below shows a _very_ simple example that returns a list of services along with their status.

```python
import ays

@ays.param(str, "url")
@ays.returns(ays.VirtualNode)
async def main(session, url):
    # TODO: Query the URL, returning the page
    # TODO: Parse the page

    # This is what the transformed values should look like
    return [
        # These are arbitrary values that you can change to your liking. You would then create
        # thresholds, on this monitor, that would trigger based on the values returned here.
        ays.VirtualNode("trello", 7), # 7 could mean 'Degraded Performance'
        ays.VirtualNode("jira", 10), # 10 could mean 'Operational'
        ays.VirtualNode("confluence", 10),
    ]
```

Again, this return value is used in contexts where only _one_ health value is associated to each virtual node.

Using our Fleet Management use case, below shows a _very_ simple example that returns a list of trucks, along with each truck's respective monitor values, queried from a database.

```python
import ays

@ays.param(str, "ip_address")
@ays.param(str, "database")
@ays.returns(ays.VirtualElder)
async def main(session, ip_address, database):
    # TODO: Connect to database
    # TODO: Map table rows to `VirtualNode`s

    # When returning multiple values, @ys needs to know what position each value
    # represents. The `ays.VirtualElder` type allows us to define this
    # relationship.
    #
    # The value for `monitors` can be a static list of monitors.
    # The value for `nodes` will contain your transformed values.
    return ays.VirtualElder(
        # These field names are used to filter values to respective sibling measurements
        names: [
            "idle", # How long truck is idling, in minutes
            "burn", # GPH burn rate
            "fuel", # Percent fuel remaining in tank
        ],
        nodes: [
            # The monitor values share the same index as their respective field above
            # e.g. Index 0 = idle, 1 = burn, 2 = fuel
            ays.VirtualNode("TWA-0001", [0, 16.0, 87]),
            ays.VirtualNode("TWA-0002", [4, 13.0, 60]),
            ays.VirtualNode("TCA-0001", [0, 15.45, 45]),
        ]
    ]
```

Three additional sibling monitors would live next to the primary (elder) monitor (the monitor shown above). Each of the sibling monitors will reference the respective field they are interested in. Such as `idle`, `burn`, or `fuel`.

Now, every truck will track its respective `idle`, `burn`, and `fuel` rate.

If you want to track different types of vehicles, but use the same monitors, create a template node with the above monitor. Then, create a node for each vehicle type that templates from this. This will allow you to tune the threshold trigger values for each respective vehicle type.
