---
title: "How to Understand Measurement Health"
date: 2023-03-23T14:18:07-07:00
draft: false
---

# How to Understand Measurement Health

A node's measurement graphs can be viewed by long-pressing on a Node and tapping the "Measure" button.

![Node Measurement Graphs](/help/img/node-measurement-graphs.gif)

Here you can see each measurement's samples over time.

Things to note:
- Measurement threshold(s) may **not** be visible if your samples are well below/above the respective threshold
- Samples that have a `0` and a red triangle are indicative of a script error. To fix this issue:
  - Make sure all [Node properties]({{< relref "library/what-is-a-node-property.md" >}}) are set. Some measurements, especially template measurements, require node properties to function. For example, a measurement script may have a `host` parameter which requires the respective `host` node property to be set.
  - If your sensor is a script, "Run" your sensor script to see if errors are returned from the server. Please [click here]({{< relref "library/how-do-i-configure-a-measurement-sensor.md" >}}) to learn how to configure your sensor script.
  - [Contact your **@ys** representative]({{< relref "library/contact-ays-representative.md" >}})
