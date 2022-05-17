---
title: "What Is a Node Relationship?"
date: 2022-05-17T09:45:02-07:00
draft: false
---

# Node Relationships

Node relationships are the logical groupings of parent and children nodes, and the dependent relationships between nodes.

Parent / child relationships are a typical [Tree data structure](https://en.wikipedia.org/wiki/Tree_(data_structure)).

Dependent relationships are defined by a node A depending on another node B for its operation. Imagine you are building a retail app that sells shoes. Your app may depend on a "Product" service, which gives you SKU level detail about your shoes, and a "Checkout" service which allows you to purchase a pair of shoes.

The following graph shows the relationship between your "iOS" retail app and the services it depends on.

```
        Acme Corp.
        /       \
    Mobile     Server
     /            \
   iOS  ------>  Product
           |-->  Checkout

Dependent      Dependencies
```

"Acme Corp." is the "Organization Node." "Mobile" and "Server" are parent nodes that provide a logical grouping of apps and services. "iOS" is a child to "Mobile", while "Product" and "Checkout" are children to "Server." "iOS" depends on the "Product" and "Checkout" service.
