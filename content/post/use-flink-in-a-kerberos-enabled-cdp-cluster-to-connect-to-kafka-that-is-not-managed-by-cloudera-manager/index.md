---
title: Use Flink in a kerberos-enabled CDP cluster to connect to Kafka that is
  not managed by Cloudera Manager
date: 2021-08-28T03:15:32.655Z
summary: >-
  A customer asked: How to use Flink in CDP to connect to Kafka that is not in
  the cluster (that is, this Kafka cluster is not managed by Cloudera Manager).


  I tried to find related Flink demos in Cloudera's official Github repository.


  In general, whether it is Flink or Spark, as a client connecting to Kafka, they must use one of the centralized protocols specified by Kafka.
draft: false
featured: false
authors:
  - admin
tags:
  - Flink
categories:
  - Big Data
image:
  filename: featured.jpeg
  focal_point: Smart
  preview_only: false
---
This article is reproduced from Cloudera Community, the original link:

🔗[在启用kerberos的集群flink程序如何连接集群外未启用认证的kafka](https://community.cloudera.com/t5/Support-Questions/%E5%9C%A8%E5%90%AF%E7%94%A8kerberos%E7%9A%84%E9%9B%86%E7%BE%A4flink%E7%A8%8B%E5%BA%8F%E5%A6%82%E4%BD%95%E8%BF%9E%E6%8E%A5%E9%9B%86%E7%BE%A4%E5%A4%96%E6%9C%AA%E5%90%AF%E7%94%A8%E8%AE%A4%E8%AF%81%E7%9A%84kafka/m-p/322981#M228986)



## Summary of this article

A customer asked: How to use Flink in CDP to connect to Kafka that is not in the cluster (that is, this Kafka cluster is not managed by Cloudera Manager).

I tried to find related Flink demos in Cloudera's official Github repository.

In general, whether it is Flink or Spark, as a client connecting to Kafka, they must use one of the centralized protocols specified by Kafka.

## Main Body of this artile

Basically, the Flink connection to Kafka also follows the pattern of using Kafka in regular Java projects. You can refer to [this link](https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/kafka-developing-applications/topics/kafka-develop-java-security-example.html#autoId0) to learn about the main options when connecting a regular Java client with Kafka.

If your non-CM managed Kafka cluster is not enabled for authentication, it should belong to "Unsecured".

I found a [demo project of Flink ↔ Kafka](https://github.com/cloudera/flink-tutorials/tree/1.12-csa1.4.0.0/flink-stateful-tutorial#setting-up-kafka-inputs-and-outputs) on Cloudera's official Github, you can refer to [job.properties](https://github.com/cloudera/flink-tutorials/blob/1.12-csa1.4.0.0/flink-stateful-tutorial/config/job.properties).

In addition, this project also has a demo project for [connecting to secure Kafka](https://github.com/cloudera/flink-tutorials), which has a part of configuring the [connection to Kafka](https://github.com/cloudera/flink-tutorials/tree/1.12-csa1.4.0.0/flink-secure-tutorial#jobproperties).

You can see that the job.properties file defines:

`kafka.security.protocol=SASL_SSL`

The meaning of this **SASL_SSL** is: Use **SASL/PLAIN** (Kafka in CDP to enable Kerberos authentication refer to [this link](https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/kafka-securing/topics/kafka-secure-kerberos-enable.html)) as the authentication method, and use **SSL/TLS** as the data transmission method (that is, in addition to the authentication configured, it also **Enable TLS/SSL for Kafka Broker** in the CM UI ). Reference: [Confluent official documentation](https://docs.confluent.io/platform/current/security/security_tutorial.html#configure-brokers).

If the transmission method does not have **Enable TLS/SSL**, then in the Kafka Broker log (/var/log/kafka/server.log), you will see **listeners = SASL_PLAINTEXT**; if **Kerberos** authentication (or other SASL authentication such as **LDAP, PAM**, etc.) is enabled, and **Enable TLS/SSL for Kafka Broker** is valid, then you will see **listeners = SASL_SSL**.

In addition, it is worth noting that you can configure multiple listeners at the same time, that is, **listeners = SASL_PLAINTEXT** and **listeners = SASL_SSL** can exist at the same time.

In addition, this demo code also has a 🎥[YouTube video demonstration](https://youtu.be/b_w0WoWuuIM).

The above information is for your reference.