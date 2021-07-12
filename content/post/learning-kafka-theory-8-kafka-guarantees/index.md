---
title: Learning Kafka | Theory-9 | Kafka Guarantees
date: 2021-07-12T01:10:36.045Z
summary: >-
  Messages are appended to a topic-partition in the order they are sent.

  Consumers read messages in the order stored in a topic-partition.

  With a replication factor of N, producers and consumers can tolerate up to N-1 brokers being down.

  This is why a replication factor of 3 is a good idea: Allows for one broker to be taken down for maintenance; Allows for another broker to be taken down unexpectedly.

  As long as the number of partitions remains constant for a topic (no new partitions), the same key will always go to the same partition.
draft: false
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
  alt_text: There are guarantees in Kafka, these guarantees are like the basic
    principles in the way of working and cannot be changed. If we want to change
    the way we work, we must change based on these principles.
---
Okay, so we're done with the theory, almost done, but I wanna mention, or reiterate, the Kafka guarantees, because they're super-important.

## Kafka Guarantees

- Messages are appended to a topic-partition in the order they are sent
- Consumers read messages in the order stored in a topic-partition
- With a replication factor of N, producers and consumers can tolerate up to N-1 brokers being down
- This is why a replication factor of 3 is a good idea:
  - Allows for one broker to be taken down for maintenance
  - Allows for another broker to be taken down unexpectedly
- As long as the number of partitions remains constant for a topic (no new partitions), the same key will always go to the same partition

The messages are appended to a topic-partition in the order they're sent.
And that's really important.
The consumers will also read these messages in the order they're stored.
So these ordering are super, super important.

And there are guarantees about Kafka.

When you have a replication factor of N, so N could be like three, for example, then producers and consumers can tolerate up to N minus one broker being down.
And that's the whole idea of replication.
So if we set a replication factor of three, for example, it's a good idea because one broker can be taken down for maintenance, and another broker can be taken down unexpectedly, and we'll still have a working topic.

So as long as the number of partitions remain constant for a topic, and remember this, as long as the number of partitions remain constant, so you don't add new partitions, then the same key will always go to the same partition.
So super-important.
So that's it for guarantees.

Remember them, but in practice, you'll remember them, I promise.
And then, I will see you in the next lecture.