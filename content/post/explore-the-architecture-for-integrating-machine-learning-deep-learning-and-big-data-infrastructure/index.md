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

## Source of this note

- 🔗[How does iQiyi effectively integrate big data and artificial intelligence platforms(Chinese)?](https://mp.weixin.qq.com/s?__biz=MjM5MDE0Mjc4MA==&mid=2651090838&idx=2&sn=5ca7b596a0bbad5722eaca6d4b3b8a62&chksm=bdb997c58ace1ed31adf1c615dabbdf1c38a6e14d0a80fd2b1ffddf6b02de61bd544dc4bf97f&scene=126&sessionid=1632192660&key=989b87583a3e3be30f24a2d95343aac616273550965f48ba57ec7ec36fa2ed0a3eeb54c7bd5d4a5e2947ded6a42d92012a69b354721d48af9e88b81ea9c58e36766eb3ddd5ab55e34f87afae8d839f5a7b0ed75ccde23c1b8e8ec5632cbb3229641dd3195802061ad81e24a7b06a8f1a22b5045d34dad1e1518f8178149f2fff&ascene=1&uin=OTIzMDA5Mzgw&devicetype=Windows+10+x64&version=63030532&lang=zh_CN&exportkey=Ay%2BM35m%2FC4zJG%2FoPeFmPXM4%3D&pass_ticket=5MfMg8XYXJQW%2BE8xamjxHldxY%2FAGEY66iHuLsJYnZ7T5aQrY%2BOUn5SwhQhecDVXL&wx_header=0&fontgear=2)
- 📹[Machine Learning with TensorFlow and PyTorch on Apache Hadoop using Cloud Dataproc (Cloud Next '19)](https://youtu.be/hr7_pG3yEOQ)
- 🔗[HDFS on Kubernetes—Lessons Learned](https://databricks.com/session/hdfs-on-kubernetes-lessons-learned)
- 🔗[Implementing distributed model training for deep learning with Cloudera Machine Learning](https://blog.cloudera.com/implementing-distributed-model-training-for-deep-learning-with-cloudera-machine-learning/)

## My thoughts about this topic

First of all, I want to introduce why I picked these materials to cut into today's main body.



When I saw the descriptions mentioned in the [interview with iQiyi][iQiyiInterview] that "it is necessary to support distributed operation of machine learning framework on Hadoop" and "the core problem is the integration of data and computing", I first thought of my current understanding of the big data ecosystem. I understand the process of data analysis in the circle, but how can the data obtained from data analysis be fed to machine learning/deep learning applications such as SparkMLlib, TensorFlow, and PyTorch?

I know Cloudera's [CDP starts to support Spark MLlib][CDPSparkMLlib], so this can be seen as a Native Hadoop-based machine learning approach.
Because Spark is so popular and endorsed by DataBricks, I believe that there is no need to worry about its popularity in the next few years.

So the question comes to how deep learning frameworks such as **TensorFlow** can get the data generated by Hadoop.



So I found Google Cloud's [DataProc's Solution][DataProcandAI] to understand how Google does this.



Then I wanted to know if Cloudera has introduced any cases in this area, so I found this [Cloudera blog post][DistributedModelTraininginCML].



Finally, I want to know how Hadoop and Kubernetes are integrated, such as whether to implement Hadoop as a StorageClass available in Kubernetes for the machine learning/deep learning applications running in Kubernetes to read data.

I have a conjecture of a platform.

If I can realize the integration of artificial intelligence and big data in the local environment, it may have the following structure:



- The big data platform adopts CDP. CDP combines some IoT devices and NiFi-based edge flow products developed by Cloudera to complete data collection. Data processing is of course done in CDP. Feeding the processed data to the machine learning can be done using SparkMLlib.
- Deep learning (TensorFlow, PyTorch, and other frameworks) was not born in combination with the Hadoop ecosystem, but they are born to work with the cloud-native ecosystem. Therefore, the AI ​​platform should adopt a Kubernetes-based solution. For example, **KubeFlow** is a cloud-native solution led by Google.
- I think it is natural to come up with a question, how do the deep learning applications of the Kubernetes cluster get the data generated by CDP? Because Kubernetes implements an abstract API, it is natural for me to think that as long as there is a Kubernetes Storage Class with Hadoop as the backend, it is enough. I think this may be one of the important reasons. Although iQiyi currently does not seem to put TensorFlow and PyTorch on Kubernetes, the advantage of separation of computing and storage is to facilitate the migration of applications to other platforms. Maybe in the future they will adopt a deep learning platform based on Kubernetes.
- If cloud-based storage (S3, etc.) is originally used locally, then it should be said that the above concern does not exist. But in most cases, we are still using the Hadoop file system, so I would like to learn about solutions in this area.
- Cloudera's Private Cloud series products are integrated with OpenShift. I guess that CDSW/CML should also has implemented integration on how to obtain data from Hadoop.

So I found this article by DataBricks - [HDFS on Kubernetes Lessons Learned][HdfsOnKubernetes—lessonsLearned], trying to understand the general methodology of Hadoop and Kubernetes integration.


It is not difficult to find that the connection between them is how Hadoop and Kubernetes should be integrated.



Because CDP Private Cloud + CDSW/CML ➡ Hadoop + Openshift ➡ Hadoop + Kubernetes.

[iQiyiInterview]: https://mp.weixin.qq.com/s?__biz=MjM5MDE0Mjc4MA==&mid=2651090838&idx=2&sn=5ca7b596a0bbad5722eaca6d4b3b8a62&chksm=bdb997c58ace1ed31adf1c615dabbdf1c38a6e14d0a80fd2b1ffddf6b02de61bd544dc4bf97f&scene=126&sessionid=1632192660&key=989b87583a3e3be30f24a2d95343aac616273550965f48ba57ec7ec36fa2ed0a3eeb54c7bd5d4a5e2947ded6a42d92012a69b354721d48af9e88b81ea9c58e36766eb3ddd5ab55e34f87afae8d839f5a7b0ed75ccde23c1b8e8ec5632cbb3229641dd3195802061ad81e24a7b06a8f1a22b5045d34dad1e1518f8178149f2fff&ascene=1&uin=OTIzMDA5Mzgw&devicetype=Windows+10+x64&version=63030532&lang=zh_CN&exportkey=Ay%2BM35m%2FC4zJG%2FoPeFmPXM4%3D&pass_ticket=5MfMg8XYXJQW%2BE8xamjxHldxY%2FAGEY66iHuLsJYnZ7T5aQrY%2BOUn5SwhQhecDVXL&wx_header=0&fontgear=2
[CDPSparkMLlib]: https://docs.cloudera.com/cdp-private-cloud-base/7.1.6/developing-spark-applications/topics/spark-mllib.html
[DataProcandAI]: https://youtu.be/hr7_pG3yEOQ
[DistributedModelTraininginCML]: https://blog.cloudera.com/implementing-distributed-model-training-for-deep-learning-with-cloudera-machine-learning/
[HdfsOnKubernetes—lessonsLearned]: https://databricks.com/session/hdfs-on-kubernetes-lessons-learned