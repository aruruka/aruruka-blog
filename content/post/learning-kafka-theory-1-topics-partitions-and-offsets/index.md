---
title: Learning Kafka | Theory-1 | Topics, Partitions and Offsets
date: 2021-05-22T11:48:46.131Z
draft: true
featured: false
authors:
  - admin
tags:
  - Kafka
categories:
  - Big Data
image:
  filename: kafka_logo.png
  focal_point: Smart
  preview_only: false
  alt_text: We need to be very familiar with the basic concepts of Kafka to be
    proficient in troubleshooting. This article explains what Topics, Partitions
    and Offsets are.
---
## Kafka Basic Theory

### <ins>Topic</ins>: a particular stream of data

**The Topic in Kafka is going to be the base of everything.**

* Similar to a table in a database (without all the constraints)
* You can have as many topics as you want
* A topic is identified by its <ins>name</ins>

### Topics are split in <ins>Partitions</ins>

Partitions is something concrete.

For example, for this one topic in the bottom, we can have three partitions.
And these three partitions have numbers, and these numbers start at zero and go all the way to whatever.

* Each Partition is ordered
* Each message within a partition gets an incremental id, called <ins>offset</ins>

![Kafka Partition](kafka_partition.png "Kafka Partition")

So as you can see, Partition 0, Partition 1 and Partition 2, in my example, they are not going to have the same number of messages.

It's **independence**.

**You can also see that the Offsets 0, does not mean anything on its own.**

It needs to be Kafka topic, blah blah blah, Partition 0, Offset 0, for it to make sense.
