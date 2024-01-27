---
title: "What Is a Node Api"
date: 2024-01-26T14:59:42-08:00
draft: false
---

# What is a Node API?

A node API is a collection of functions, that belong to a node, that can be executed from within **@ys**.

These functions provide a way to interact with the respective service or machine that the node represents. Some examples of what a node API can be used for:

- Perform administrative functions on a service or machine. e.g. restart a service or machine.
- Send firmware updates to hundreds of IoT devices
- Send configuration parameters to hundreds of IoT devices

## The Anatomy of a Node API function

Node API functions use the `asyncio` library for asynchronous operations.

```python
# The `api` library provides the decorators and APIs that drive Node APIs
import api

# This is a type of data source. It provides a list of firmware versions that a
# user will select from before executing the API.
def list_options():
    return [
        ("1.0.0 b43", "https://www.example.com/fw/1_0_0b43.pkg"),
        ("1.2.3 b150", "https://www.example.com/fw/1_2_3b150.pkg"),
    ]

# Define the parameter(s) that can be sent to your function. Parameter types
# can be an `int`, `str`, `float`, or `bool`.
# Data source options are always a `str` type.
@param(str, "version", source=list_options)
# The `name` parameter is a (required) displayable name for your function.
@name("Upload firmware")
aysnc def upload_firmware(session, version):
    # Send a log to the client
    await session.log(f"The value of version ({version})")
    # Returns the `Node` this API belongs to. For example, if this API belongs
    # to the `com.example.web` node, this will return a `Node` model that
    # has all properties of the `com.example.web` node.
    node = session.get_node()
    # Returns all children nodes of this node. Useful when a child represents
    # a service or machine you want to send commands to.
    children = session.get_children()
    num_children = len(children)
    # Send a status message to client. The status message allows you to inform the
    # client the current job #, the total number of jobs, and the description of
    # the job being performed.
    await session.status(0, num_children, "Initializing firmware updates")
    for idx, child in enumerate(children):
        # Returns a property associated to the node.
        ip_address = session.get_property("ip_address", node)
        await session.status(idx + 1, num_children, f"Sending firmware update to: {ip_address}")
        # TODO: Send the update here
    # Like `get_children`, you can also query for any grand child that belongs
    # to this node.
    grand_children = session.get_children_for(children[0].id)
```

## API: `api.Session`

The `api.Session` provides a way to send logs, statuses, and get information about nodes within the current context.

`log(message: str) -> None` - Send a log message to the client

`status(current_job: int, total_jobs: int, message: str) -> None` - Send a status update to the client

`get_children() -> [node_pb2.Node]` - Returns a list of children nodes that belong to the parent node

`get_children_for(node_id: str) -> [node_pb2.Node]` - Returns children that belong to the node

## API: `@param` Decorator

The `@param` decorator defines a parameter that can be sent to the respective function. A parameter can also be configured to be auto-populated with the following values:

- Software key
- Global software key
- A data source which provides options to choose from

### Software Key

To configure a parameter to use a software key, please do the following:

```python
@param(str, "software_key", key=1)
```

`key` references the ID of the software key. To find the respective software key ID, the IDE provides a `Keys` menu option. Tap the `Keys` menu option to list all available software keys. Find the software key's ID from the list and set the value to the `key` parameter.

### Global Software Key

To configure a parameter to use a global software key, please do the following:

```python
@param(str, "software_key", global_key=10)
```

The `global_key` value of `10` references the ID of a global software key. To find the respective global software key, the IDE provides a `Keys` menu option. Tap the `Keys` menu option to list all available global software keys. Find the global software key's ID from the list and set the value to the `global_key` parameter.

### Data Source

A data source allows you to query a (remote) data source for a list of name / value pairs that will be presented to the user as a drop-down of options. A data source can currently be:

- A reference to a Python function
- Download a CSV, JSON, or YAML file via HTTP
- MySQL
- PostgreSQL

**Configure a Python function reference**

```python
def list_options():
    return [
        ("1.0.0 b43", "https://www.example.com/fw/1_0_0b43.pkg"),
        ("1.2.3 b150", "https://www.example.com/fw/1_2_3b150.pkg"),
    ]

@param(str, "version", source=list_options)
```

The first value of the tuple provides the displayable value of the option (the "name") a user will see in a drop-down. The second value is the value that is passed to the function when the option is selected.

**Configure a MySQL database**

```python
@param(str, "version", api.MySQLSource("192.168.0.1", "my_db", "username", "password", "table", "name_col", "value_col"))
```

Alternatively, you can inject software keys inside data source parameters. Here is an example showing how to inject software key, with a value of `2`, as the password for the database.

```python
@param(str, "version", api.MySQLSource("192.168.0.1", "my_db", "username", "{key:2}", "table", "name_col", "value_col"))
```

Specifically, this will replace `{key:2}` with the respective software key value.

**Configure a PostgreSQL database**

This works the same as MySQL. Replace `api.MySQLSource` with `api.PostgreSQLSource`.

**Configure a HTTP data source**

The example below will download and parse a CSV file.

```python
@param(str, "version", api.HTTPSource("https://www.example.com/my_options.csv", parser=api.CSVParser()))
```

#### Parser: `CSVParser`

There must be only two columns. The first column is the displayable value. The second column the value.

#### Parser: `JSONParser`

The payload must be an array of dictionaries where each dictionary contains the keys `name` and `value`.

```json
[
    {"name": "1.0.0 b43", "value": "https://www.example.com/fw/1_0_0b43.pkg"},
    {"name": "1.2.3 b150", "value": "https://www.example.com/fw/1_2_3b150.pkg"}
]
```

#### Parser: `YAMLParser`

The payload must be an array of dictionaries where each dictionary contains the keys `name` and `value`.

```yaml
- name: 1.0.0 b43
  value: https://www.example.com/fw/1_0_0b43.pkg
- name: 1.2.3 b150
  value: https://www.example.com/fw/1_2_3b150.pkg
```
