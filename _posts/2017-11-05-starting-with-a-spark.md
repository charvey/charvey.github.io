---
layout: single
title:  "Starting with a Spark"

tags: Java Hadoop Spark Data
---

In order to get back into the [Hadoop](http://hadoop.apache.org/) and Big Data world I decided to try out [Apache Spark](https://spark.apache.org/). Apache Spark is a project in the [Hadoop family](https://hortonworks.com/ecosystems/) that is a framework for computing data across a cluster. Because Spark data stays in memory it can be much faster than just running a simple MapReduce job.

## Setup
I run Windows and Spark claims to be compatible so I decided to try to [download the latest](http://spark.apache.org/downloads.html) and [run the examples](https://spark.apache.org/docs/latest/index.html#running-the-examples-and-shell).  The only prerequisite seemed to be Java so I installed that too.
The first problem I encountered was missing the Windows utilities for Hadoop. This is a [common](http://www.srccodes.com/p/article/39/error-util-shell-failed-locate-winutils-binary-hadoop-binary-path) problem and even though [Apache doesn't offer them](https://wiki.apache.org/hadoop/WindowsProblems) for download they [link to a repository](https://github.com/steveloughran/winutils) that does.
The next issue was getting Paths and Environment variables set correctly. The [key](https://jaceklaskowski.gitbooks.io/mastering-apache-spark/spark-tips-and-tricks-running-spark-windows.html) is setting HADOOP_HOME to the folder wheere your Spark package was extracted to.
The final issue was I didn't have the [right version of Java](https://gist.github.com/lukewang1024/659ec27847169086dde8677e25156573) installed. Apparently Spark currently only works with Java 8.

After addressing the problems I was able to run the basic Pi example. However even though I was getting results, there was still an [error](https://issues.apache.org/jira/browse/SPARK-12216) because Spark couldn't cleanup temporary files. Unfortunately the only fix would be to grant generous permissions to my temp directory.

## Simple Steps
If I had to do it again, these are the actual steps that need to be followed to get Spark running on a Windows machine.
1. Download and install [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
1. Download and extract the [Spark package with Hadoop](http://spark.apache.org/downloads.html)
1. Download the [Winutils](https://github.com/steveloughran/winutils) and extract them to your Spark directory
1. Make sure HADOOP_HOME is set to the folder where the Spark package was extracted

## Lessons Learned
The Hadoop family of software is designed to run on Linux. Therefore it's probably best to use Linux when playing around with it. I'll be dusting off [VirtualBox](https://www.virtualbox.org/) to get a Linux VM running locally and might even try [Docker](https://www.docker.com).