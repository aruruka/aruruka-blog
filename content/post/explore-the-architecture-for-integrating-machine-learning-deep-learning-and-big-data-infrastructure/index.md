---
title: Explore the architecture for integrating machine learning/deep learning
  and big data infrastructure
date: 2021-09-21T05:22:54.233Z
summary: I wrote this article, which is a note on how to explore the integration
  of machine learning/deep learning and Hadoop.
draft: true
featured: false
authors:
  - admin
tags:
  - Hadoop
  - Spark
  - TensorFlow
  - PyTorch
categories:
  - Machine Learning
  - Deep Learning
  - Big Data
  - Architecture
image:
  filename: ""
  focal_point: Smart
  preview_only: false
  alt_text: I wrote this article, which is a note on how to explore the
    integration of machine learning/deep learning and Hadoop.
---
## Motivation

Today I saw an article from the InfoQ official account on WeChat.

🔗Link of the article: [How does iQiyi effectively integrate big data and artificial intelligence platforms(Chinese)?](https://mp.weixin.qq.com/s?__biz=MjM5MDE0Mjc4MA==&mid=2651090838&idx=2&sn=5ca7b596a0bbad5722eaca6d4b3b8a62&chksm=bdb997c58ace1ed31adf1c615dabbdf1c38a6e14d0a80fd2b1ffddf6b02de61bd544dc4bf97f&scene=126&sessionid=1632192660&key=989b87583a3e3be30f24a2d95343aac616273550965f48ba57ec7ec36fa2ed0a3eeb54c7bd5d4a5e2947ded6a42d92012a69b354721d48af9e88b81ea9c58e36766eb3ddd5ab55e34f87afae8d839f5a7b0ed75ccde23c1b8e8ec5632cbb3229641dd3195802061ad81e24a7b06a8f1a22b5045d34dad1e1518f8178149f2fff&ascene=1&uin=OTIzMDA5Mzgw&devicetype=Windows+10+x64&version=63030532&lang=zh_CN&exportkey=Ay%2BM35m%2FC4zJG%2FoPeFmPXM4%3D&pass_ticket=5MfMg8XYXJQW%2BE8xamjxHldxY%2FAGEY66iHuLsJYnZ7T5aQrY%2BOUn5SwhQhecDVXL&wx_header=0&fontgear=2)

This article introduced: "<ins>The core issue is the integration of data and computing.</ins>"

> Traditional machine learning puts data on a separate machine and only uses the computing resources of a single machine for model training.
> As a result, big data and AI have become two completely independent systems.
> Only by making full use of the rich storage and computing resources of the big data platform can the power of AI be fully utilized.

To be honest, I haven't thought about this thing before, because I don't know much about machine learning/deep learning.
The technical achievements that big data brings to us usually cover the well-known OLAP and BI applications. With the addition of big data technology, OLAP and BI have changed from a stand-alone architecture to a distributed computing based on a distributed storage/file system. 

Naturally, the AI field should also face technical difficulties related to distributed systems.

I have no knowledge of business logic in the AI field, and I have no foundation in mathematics and statistics, so I have no idea how machine learning/deep learning programming frameworks work logically.
Nevertheless, I still feel that I can try to understand the integration of AI and big data from the infrastructure level.

Therefore, I wrote this article, which is a note on how to explore the integration of machine learning/deep learning and Hadoop.

