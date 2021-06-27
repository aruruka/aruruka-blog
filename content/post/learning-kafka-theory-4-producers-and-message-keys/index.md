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

They're good, they're just well-programmed.

You don't have to implement that feature, it's done for you.

So here's what it looks like in real life.

So we have a producer, and it's sending data to partition zero, one and two of topic A. And now we have the source of these writes that we had before.

And so basically the producer, we'll see how it understands to which broker you send data to, but basically, if you send the without a key then data will be sent round robin to broker 101, 102 and 103.

So basically, be sending data to Kafka, to the topic, the producer will load balance.

Automatically send a little bit to broker one, a little bit to broker two, a little bit to broker three, and then switch on again. So this is how load balancing is done in Kafka.

* Producers can choose to receive acknowledgement of data writes:

  * acks=0: Producer won't wait for acknowledgement (possible data loss)
  * acks=1: Producer will wait for leader acknoledgement (limited data loss)

![kafka-theory_producers_and_message_keys-2.png](kafka-theory_producers_and_message_keys-2.png "automatic load balance by broker")

Now, if we take the exact same topic, before we go into load balancing and keys, let's look at how the producer can write.

So the producer can choose to receive acknowledgement of data writes. Acknowledgement is a synonym of confirmation. And there's three confirmation or acknoledgement modes.

Acks equals zero, which is the producer just sends the data  and you will not wait for acknoledgement. In that case there is a possible data loss.

Because if you send the data to your broker and the broker is down, but we don't know about it because we set acks equals zero and we weill not get an acknoledgement and we will lose the data, so this is tricky and we'll see examples in which acks equals zero is used but it's very dangerous.

Acks equals one is the default, which is producer will wait for the leader to acknoledge, so it sends data, for example to partition zero, to broker 101, and it says, hey, here's the data.