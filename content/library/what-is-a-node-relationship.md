---
title: "What Is a Node Relationship?"
date: 2022-05-17T09:45:02-07:00
draft: false
---

# Node Relationships

Nodes relationshiops are logically grouped by children, dependents, and their dependencies.

Parent / child relationships are a typical [Tree data structure](https://en.wikipedia.org/wiki/Tree_(data_structure)).

Dependecies and dependents allow a node to define which services, assets, etc. it depends on. Imagine you are building a retail app that sells shoes. Your app may depend on a "Product" service, which gives you SKU level detail about your shoes, and a "Checkout" service which allows you to purchase a pair of shoes.

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

"Acme Corp." is the "Organization Node." "Mobile" and "Server" a parent nodes that provide a logical grouping of apps and services. "iOS" is a child to "Mobile", while "Product" and "Checkout" are children to "Server." "iOS" is dependent on the "Product" and "Checkout" service.
