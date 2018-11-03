<!-- TOC -->

- [概念](#概念)
    - [运行时用到的概念](#运行时用到的概念)
    - [调度中的概念](#调度中的概念)

<!-- /TOC -->

# 概念

## 运行时用到的概念

应用程序(Application)：用户编写的Spark程序，包含驱动程序和分布在集群中中多个节点运行的Executor代码，在执行过程中由一个或者多个作业组成

驱动程序(Driver)：上述Application中main函数代码并创建的SparkContext，其中创建SparkContext的目的是为了准备Spark应用程序的运行环境。SparkContext负责与ClusterManager通信，进行资源的申请、任务的分配和监控等；当Executor部分运行完毕之后，Driver负责将SparkContext关闭，通常SparkContext代表Driver

集群资源管理器(Cluster Manager)：指在集群上获取资源的外部服务，目前有以下这些
* Standalone：Spark原生资源管理器，由Master负责资源管理
* Hadoop Yarn：由Yarn中的ResourceManager负责资源管理，// TODO 听过但还没研究过
* Mesos // TODO 还没了解过
* K8S // TODO 还没了解过

工作节点(Worker)：集群中任何可以运行Application代码的节点，在Standalone模式中就是Slave文件配置的Worker节点；在Spark on Yarn中就是NodeManager节点

总控进程(Master)：Standalone运行模式下的主节点，负责管理和分配集群资源来运行Spark Application

执行进程(Executor)：Application在Worker上的一个进程，负责执行Task


## 调度中的概念

作业(job)：RDD中由行动操作所生成的一个或者多个调度阶段

调度阶段(stage)：每个作业会因为RDD之间的依赖关系拆分成多组任务集合，也叫作任务集(TaskSet)。调度阶段的划分是由DAGScheduler来划分的，调度阶段有Shuffke Map Stage和Result Stage两种

任务(Task)：分发到Executor上的工作任务，是Spark实际执行应用的最小单元

DAGScheduler：面向调度阶段的任务调度器，负责接收Spark应用提交的作业，根据RDD的依赖关系划分调度阶段，并提交调度阶段给TaskScheduler

TaskScheduler：面向任务的调度器，它接收DAGScheduler提交过来的调度阶段，然后把任务分发到Work节点运行，Worker节点的Executor来运行该任务
