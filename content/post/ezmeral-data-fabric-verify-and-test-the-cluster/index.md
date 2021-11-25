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
# How to verity and test the Ezmeral Data Fabric installation

## Run synthetic benchmarks to gauge cluster performance

### DFSIO

* Use DFSIO to test read or write performance
* Syntax for DFSIO

```shell
find /opt -type f -iname '*mapreduce*client*tests.jar'
# /opt/mapr/hadoop/hadoop-2.7.4/share/hadoop/mapreduce/hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar

cd /opt/mapr/hadoop/hadoop-2.7.4/share/hadoop/mapreduce

yarn jar hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar \
TestDFSIO -write -nrFiles 10 -fileSize 1000 -resFile /tmp/DFSIO-write
```

Sample Output:

```
[root@m2-maprts-vm218-173 ~]# sudo -u mapr yarn jar hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar \
> TestDFSIO -write -nrFiles 10 -fileSize 1000 -resFile /tmp/DFSIO-write
Not a valid JAR: /tmp/hsperfdata_mapr/hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar
[root@m2-maprts-vm218-173 ~]# cd /opt/mapr/hadoop/hadoop-2.7.4/share/hadoop/mapreduce
[root@m2-maprts-vm218-173 mapreduce]# yarn jar hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar \
> TestDFSIO -write -nrFiles 10 -fileSize 1000 -resFile /tmp/DFSIO-write^C
[root@m2-maprts-vm218-173 mapreduce]# sudo -u mapr yarn jar hadoop-mapreduce-client-jobclient-2.7.4.0-mapr-700-tests.jar \
> TestDFSIO -write -nrFiles 10 -fileSize 1000 -resFile /tmp/DFSIO-write
21/11/24 21:54:07 INFO fs.TestDFSIO: TestDFSIO.1.8
21/11/24 21:54:07 INFO fs.TestDFSIO: nrFiles = 10
21/11/24 21:54:07 INFO fs.TestDFSIO: nrBytes (MB) = 1000.0
21/11/24 21:54:07 INFO fs.TestDFSIO: bufferSize = 1000000
21/11/24 21:54:07 INFO fs.TestDFSIO: baseDir = /benchmarks/TestDFSIO
21/11/24 21:54:07 INFO fs.TestDFSIO: creating control file: 1048576000 bytes, 10 files
21/11/24 21:54:07 INFO fs.TestDFSIO: created control files for: 10 files
21/11/24 21:54:08 INFO client.MapRZKBasedRMFailoverProxyProvider: Updated RM address to m2-maprts-vm218-173.mip.storage.hpecorp.net/10.163.173.218:8032
21/11/24 21:54:08 INFO client.MapRZKBasedRMFailoverProxyProvider: Updated RM address to m2-maprts-vm218-173.mip.storage.hpecorp.net/10.163.173.218:8032
21/11/24 21:54:08 INFO mapred.FileInputFormat: Total input paths to process : 10
21/11/24 21:54:08 INFO mapreduce.JobSubmitter: number of splits:10
21/11/24 21:54:08 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1637803588440_0001
21/11/24 21:54:08 INFO security.ExternalTokenManagerFactory: Initialized external token manager class - org.apache.hadoop.yarn.security.MapRTicketManager
21/11/24 21:54:09 INFO impl.YarnClientImpl: Submitted application application_1637803588440_0001
21/11/24 21:54:09 INFO mapreduce.Job: The url to track the job: http://m2-maprts-vm218-173.mip.storage.hpecorp.net:8088/proxy/application_1637803588440_0001/
21/11/24 21:54:09 INFO mapreduce.Job: Running job: job_1637803588440_0001
21/11/24 21:54:17 INFO mapreduce.Job: Job job_1637803588440_0001 running in uber mode : false
21/11/24 21:54:17 INFO mapreduce.Job:  map 0% reduce 0%
21/11/24 21:54:23 INFO mapreduce.Job:  map 10% reduce 0%
21/11/24 21:54:25 INFO mapreduce.Job:  map 20% reduce 0%
21/11/24 21:54:26 INFO mapreduce.Job:  map 30% reduce 0%
21/11/24 21:54:27 INFO mapreduce.Job:  map 40% reduce 0%
21/11/24 21:54:30 INFO mapreduce.Job:  map 50% reduce 0%
21/11/24 21:54:31 INFO mapreduce.Job:  map 60% reduce 0%
21/11/24 21:54:32 INFO mapreduce.Job:  map 70% reduce 0%
21/11/24 21:54:34 INFO mapreduce.Job:  map 80% reduce 0%
21/11/24 21:54:36 INFO mapreduce.Job:  map 90% reduce 0%
21/11/24 21:54:37 INFO mapreduce.Job:  map 100% reduce 0%
21/11/24 21:54:43 INFO mapreduce.Job:  map 100% reduce 100%
21/11/24 21:54:43 INFO mapreduce.Job: Job job_1637803588440_0001 completed successfully
21/11/24 21:54:43 INFO mapreduce.Job: Counters: 46
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=1125739
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                MAPRFS: Number of bytes read=4188
                MAPRFS: Number of bytes written=10485762082
                MAPRFS: Number of read operations=505
                MAPRFS: Number of large read operations=0
                MAPRFS: Number of write operations=1290875
        Job Counters
                Launched map tasks=10
                Launched reduce tasks=1
                Data-local map tasks=10
                Total time spent by all maps in occupied slots (ms)=38382
                Total time spent by all reduces in occupied slots (ms)=6195
                Total time spent by all map tasks (ms)=38382
                Total time spent by all reduce tasks (ms)=2065
                Total vcore-seconds taken by all map tasks=38382
                Total vcore-seconds taken by all reduce tasks=2065
                Total megabyte-seconds taken by all map tasks=39303168
                Total megabyte-seconds taken by all reduce tasks=6343680
                DISK_MILLIS_MAPS=19195
                DISK_MILLIS_REDUCES=2746
        Map-Reduce Framework
                Map input records=10
                Map output records=50
                Map output bytes=778
                Map output materialized bytes=0
                Input split bytes=1110
                Combine input records=0
                Combine output records=0
                Reduce input groups=5
                Reduce shuffle bytes=898
                Reduce input records=50
                Reduce output records=5
                Spilled Records=100
                Shuffled Maps =10
                Failed Shuffles=0
                Merged Map outputs=11
                GC time elapsed (ms)=375
                CPU time spent (ms)=24040
                Physical memory (bytes) snapshot=7670259712
                Virtual memory (bytes) snapshot=46070525952
                Total committed heap usage (bytes)=8325169152
        Shuffle Errors
                IO_ERROR=0
        File Input Format Counters
                Bytes Read=1120
        File Output Format Counters
                Bytes Written=84
21/11/24 21:54:43 INFO fs.TestDFSIO: ----- TestDFSIO ----- : write
21/11/24 21:54:43 INFO fs.TestDFSIO:            Date & time: Wed Nov 24 21:54:43 PST 2021
21/11/24 21:54:43 INFO fs.TestDFSIO:        Number of files: 10
21/11/24 21:54:43 INFO fs.TestDFSIO: Total MBytes processed: 10000.0
21/11/24 21:54:43 INFO fs.TestDFSIO:      Throughput mb/sec: 1039.8253093480296
21/11/24 21:54:43 INFO fs.TestDFSIO: Average IO rate mb/sec: 1375.8668212890625
21/11/24 21:54:43 INFO fs.TestDFSIO:  IO rate std deviation: 510.54283862956197
21/11/24 21:54:43 INFO fs.TestDFSIO:     Test exec time sec: 35.256
21/11/24 21:54:43 INFO fs.TestDFSIO:
[root@m2-maprts-vm218-173 mapreduce]#

```

- DFSIO can be used with –write or –read (must use –write first)
- Compare DFSIO results to pre-installation performance
- Measure storage performance using DFSIO and compare to what was expected based on pre-install tests
- Reasonable starting performance: DFSIO results at least 50% of maximum from disk-test.sh