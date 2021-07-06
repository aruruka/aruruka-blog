---
title: Learning Kafka | Theory-5 | Consumers and Consumer Groups
date: 2021-07-06T19:46:14.788Z
summary: >-
  Now, we're getting into the very important concept of consumers.


  We know about producers, but now things need to read data, so here is consumers.
draft: true
featured: false
authors:
  - admin
tags:
  - Kafka
categories:
  - Big Data
image:
  filename: featured.png
  focal_point: Smart
  preview_only: false
  caption: ""
  alt_text: If you want to have high number of consumers, you need to have a high
    number of partitions.
---
## Consumers

Now, we're getting into the very important concept of consumers.

We know about producers, but now things need to read data, so here is consumers.

* Consumers read data from a topic (identified by name)
* Consumers know which broker to read from
* In case of broker failures, consumers know how to recover
* Data is read in order <ins>**within each partitions**</ins>

As we said, consumers will read data from a topic, and the topic is going to be identified by its name. The consumers, they know which broker to read from automatically, it's already programmed for you, and, in case of broker failures, just like producers, the consumers will know how to recover. This is already done for you. You don't have to think about this. Data, overall, will be read in order within each partition.
So we'll see what that means right now.

We have Broker 101 and Topic-A Partition Zero, and we have a consumer reading from it.
It's going to read data. So as I said, it's going to read data in order.
I will read message zero, or Offset Zero, then Offset One, Offset two, et cetera, et cetera, up to Offset 11.