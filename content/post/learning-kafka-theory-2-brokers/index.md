---
title: Learning Kafka | Theory-2 | Brokers
date: 2021-05-26T05:25:45.056Z
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
  alt_text: This article explains the relationship between Broker and Topic in Kafka.
---
## Brokers

* A Kafka cluster is composed of multiple brokers(servers)
* Each Broker is identified with its ID(integer)
* Each Broker contains certain topic partitions
* After connecting to any Broker (called a bootstrap broker), you will be connected to the entire cluster
* A good number to get started is 3 Brokers, but some big clusters have over 100 Brokers
* In these examples we choose to number Brokers starting at 100 (arbitrary)

OK, so we've talked about Topics, but what holds the Topics? What holds the Partitions?

And the answer is a Broker.

So, we may have heard the term before, it's called a Kafka cluster.
And cluster means that it's comprised, composed of multiple Brokers and each Broker is basically a server, okay?

So, when a cluster use multiple machine, broker means server.

So in the bottom I have three brokers;

![](kafka-theory_broker.png "Kafka theory - Brokers")

I have Broker 101, Broker 102 and Broker 103. But the number is arbitrary. You could be 123, you could be whatever you want.

So, the ID is going to be a number. You cannot have a Broker - "My Broker". It has to be a number.

Now, each Broker will contain only certain topic partitions.

So, we'll see how they get this onto the next slide. But basically, each Broker has some kind of data, but not all the data, okay?

Because Kafka is distributed.

Something there's a whole lecture dedicated on it, but just know about it.

When you connect to one Broker or any Broker that called bootstrap broker, you're connected to the entire cluster.

So in Kafka, when you connected to one Kafka Broker, you're connected to a cluster. Even if you have one hundred Brokers in it.

We'll see how that works later on.

When you get started to Kafka and create a cluster, a good number is three regarding the number of brokers.

But some big clusters of some huge companies do have up to 100 Brokers and that's expected, okay?