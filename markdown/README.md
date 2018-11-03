<!-- TOC -->

- [摘要](#摘要)
    - [下载安装](#下载安装)
    - [Spark概念](#spark概念)
    - [RDD](#rdd)
    - [存储模型](#存储模型)
    - [通信机制](#通信机制)
    - [内存模型](#内存模型)
    - [调度原理](#调度原理)
    - [Spark SQL](#spark-sql)
    - [对一些问题的思考](#对一些问题的思考)

<!-- /TOC -->

# 摘要

这里主要记录一下每一部分的简要概述

## 下载安装

在学习Spark之前，免不了需要手动下载Spark源码，手动编译，配置环境等步骤。[这里](https://github.com/MyXOF/SparkNotes/blob/master/markdown/install.md)介绍一下必要的步骤。


## Spark概念

一些Spark里面常用概念的说明，作为背景知识。

* RDD(Resilient Distributed Dataset)
* Cluster, Master, Slaver
* Application, Driver, Executor, Worker
* DAG, Stage, Job, Task

每一个概念更为详细的介绍请移步[这里](https://github.com/MyXOF/SparkNotes/blob/master/markdown/concept.md)。

## RDD



## 存储模型

// TODO

## 通信机制

// TODO

## 内存模型

// TODO

## 调度原理

Spark的作业调度主要基于RDD的一系列操作构成的一个作业，然后在Executor中执行，调度中最重要的是DAGScheduler和TaskScheduler调度器，DAG负责逻辑上的调度，Task负责具体任务的调度执行，大致流程如下：

1. 在触发action操作之后，首先需要根据RDD的关系依赖图构建DAG图，提交给DAGScheduler进行解析

2. DAGScheduler根据宽窄依赖进行切分，切分之后的基本单元就是stage，即调度阶段。一个调度包含一个或者多个任务，统称为一个任务集。一个任集合会提交给TaskScheduler进行调度。

3. 除此之外，DAGScheduler还会记录哪些RDD被存入磁盘等物化操作，同时要寻求任务的最优化调度，如数据本地性；DAGScheduler监控运行调度阶段过程，如果某个调度运行失败，则需要重新提交该调度阶段

4. 每个TaskScheduler只为一个SparkContext实例服务，TaskScheduler接受DAGScheduler发送过来的任务集，对任务集进行调度，每次将一个任务分发到不同的worker节点上，执行所对应的分区的计算，如果某个任务失败了，TaskScheduler要负责重新提交该任务，如果一个任务一直没有运行完(拖后腿)的，要再让另一个worker跑同样的任务，谁先跑完用谁的结果，和MR on hadoop的思想类似。

5. worker中的Executor收到TaskScheduler发送过来的任务后，以多线程的方式运行，每个线程负责一个任务。任务结束以后要返回给TaskScheduler，不同类型的任务，返回的方式也不同，ShuffleMapTask返回的是一个MapStatus对象，而不是结果本身。ResultTask根据结果的大小不同，返回的方式也不相同

细节在架构篇中会结合源代码具体分析

## Spark SQL

// TODO


## 对一些问题的思考

记录一些偶然想到的问题和不理解的地方，请移步[这里](https://github.com/MyXOF/SparkNotes/blob/master/markdown/QA.md)。

