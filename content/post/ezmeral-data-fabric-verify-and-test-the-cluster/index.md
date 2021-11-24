---
title: Ezmeral Data Fabric | Verify and Test the Cluster
date: 2021-11-24T05:22:40.627Z
draft: true
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
```shell
find /opt -type f -iname '*mapreduce*client*tests.jar'
# /opt/mapr/hadoop/hadoop-2.7.4/share/hadoop/mapreduce/hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar

cd /opt/mapr/hadoop/hadoop-2.7.4/share/hadoop/mapreduce

yarn jar hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar \
TestDFSIO -write -nrFiles 10 -fileSize 1000 -resFile /tmp/DFSIO-write
```

# How to verity and test the Ezmeral Data Fabric installation

## Run synthetic benchmarks to gauge cluster performance

### DFSIO

* Use DFSIO to test read or write performance
* Syntax for DFSIO