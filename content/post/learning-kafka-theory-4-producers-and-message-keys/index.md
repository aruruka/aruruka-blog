---
title: Learning Kafka | Theory-4 | Producers and Message Keys
date: 2021-06-20T14:33:33.822Z
summary: >-
  Okay, so we know all about topics, we know all about brokers, we know about
  replication, but now how do we get data into Kafka?


  Well, that's the role of a Producer.


  This article attempts to explain what Kafka's Producer is.
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
  focal_point: TOPRIGHT
  preview_only: false
---
Okay, so we know all about topics, we know all about brokers, we know about replication, but now how do we get data into Kafka?

Well, that's the role of a Producer.

## Producers

* Producers write data to topics (which is made of partitions)
* Producers automatically know to which broker and partition to write to
* In case of Broker failures, Producers will automatically recover

![kafka-theory_producers_and_message_keys-1.png](kafka-theory_producers_and_message_keys-1.png "The load is balanced to many brokers thanks to the number of partitions")

And producers, they will write data to topics and the topics again are made of partitions, so producers are kind of migical, but people who write producers to clients will use is that producers automatically know which broker and partition to write to, we don't have to specify that.

And so for you, that removes a lot of the burden, you just connect to Kafka and then the producers automatically know to which broker and partition to write to.

When there's a broker failure, for example, and the broker goes down as we see in the previous example, the producers, they will automatically recover.