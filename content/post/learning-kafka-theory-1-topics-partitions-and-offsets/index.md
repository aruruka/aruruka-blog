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
  filename: https://cdn.icon-icons.com/icons2/2248/PNG/512/apache_kafka_icon_138937.png
  focal_point: Smart
  preview_only: false
  alt_text: We need to be very familiar with the basic concepts of Kafka to be
    proficient in troubleshooting. This article explains what Topics, Partitions
    and Offsets are.
---
## Kafka Basic Theory

### <ins>Topic</ins>: a particular stream of data

**The Topic in Kafka is going to be the base of everything.**

- Similar to a table in a database (without all the constraints)
- You can have as many topics as you want
- A topic is identified by its <ins>name</ins>

### Topics are split in <ins>Partitions</ins>

Partitions is something concrete.

For example, for this one topic in the bottom, we can have three partitions.
And these three partitions have numbers, and these numbers start at zero and go all the way to whatever.

- Each Partition is ordered
- Each message within a partition gets an incremental id, called <ins>offset</ins>
