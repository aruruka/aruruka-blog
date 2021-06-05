---
title: Learning Kafka | Theory-3 | Topic Replication
date: 2021-06-05T06:14:43.149Z
summary: >-
  As you've seen, Kafka is a distributed system.


  We may have three Brokers or one hundred Brokers, so this is distributed.


  So, when there's a distributed system in the big data world, we need to have replication, such as,


  if a machine goes down, then the things still work, and replication does that for us.
draft: true
featured: false
authors:
  - Raymond Yan
tags:
  - Kafka
categories:
  - Big Data
image:
  filename: featured.png
  focal_point: Smart
  preview_only: false
  alt_text: As you've seen, Kafka is a distributed system.  We may have three
    Brokers or one hundred Brokers, so this is distributed.  So, when there's a
    distributed system in the big data world, we need to have replication, such
    as,  if a machine goes down, then the things still work, and replication
    does that for us.
---
## Topic Replication Factor

As you've seen, Kafka is a distributed system.

We may have three Brokers or one hundred Brokers, so this is distributed.

So, when there's a distributed system in the big data world, we need to have replication, such as,

if a machine goes down, then the things still work, and replication does that for us.

- - -

* Topics should have a replication factor > than 1 (usually between 2 and 3)
* This way if a Broker is down, another Broker can serve the data
* Example: Topic-A with 2 partitions and replication factor of 2

![](kafka-theory_topic_replication-1.png "Diagram-1: Example: Topic-A with 2 partitions and replication factor of 2")

Here is an example, hands-on.

We are going to have Topic-A with 2 partitions. Partition 0 got assigned to Broker 101 and Partition 1 got assigned to Broker 102.

Because there's a replication factor of two, we need to see two replicas of these partitions somewhere.

Partition 0 of Topic-A is also going to be replicated on Broker 102