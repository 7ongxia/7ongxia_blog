---
title: "Chapter 1. Intro to Google Cloud Platform"
date: 2021-08-10T16:53:53+08:00
draft: true
toc: true
tags:
  - Cloud
  - GCP
  - 빠르게 훑어보는 구글 클라우드 플랫폼
---

Google Cloud Platform(GCP) is a global cloud service which provides Compute, Storage, Networking, Big Data, Machine learning and etc, based on Google's Data Centre infrastructures.

{{< image src="/GCP/GCP_portfolio.png" alt="view" position="left" style="border-radius: 8px; width: 100%; margin-bottom: 10px;" >}}

Compute service provides
- IaaS, bases on VM: Compute Engine
- PaaS: App Engine
- Docker runtime, based on Kubernetes: Container Engine

GCP's unique characteristics can be summarized into three points.

1. Big Data and Machine Learning services
2. Global Coverage using Google Private Network
3. Reasonable price model


## 1. Big Data and Machine Learning services

### 1.1. Big Data Analysis platform

Big Data platform services Data Collection, Processing and Storing to analyze data. 

**BigQuery**

BigQuery is a large-scale Data storage and analysis platform, kind of a data warehouse. Using 8,800 CPUs and 3,600 Disks, BigQuery can run a query in 30 seconds for 100 billion records. Cheap, and also easy to use. (Grammar is similar to SQL)

**Dataflow**

Dataflow is a platform based on open source framework, Apache Beam, for Real-Time streaming analysis and batch processing, like Apache Spark or Flink. Converts collected data or routes among data sources and storages.

**Pub/Sub Queue**

Pub/Sub is a large-scale queueing system like Kafka, collects data on a large-scale.

**Cloud Datalab**

Datalab is a web based tool which availables Data Scientists and Engineers to access various data sources and work in an environment like MS Words, and run queries directly by connecting to BigQuery from Datalab. Also can be worked by using MarkUp, like Wiki. Similar to open source "Jupyter".

**Dataproc**




### 1.2. Machine Learning platform


## 2. Global Coverage using Google Private Network


## 3. Reasonable price model

