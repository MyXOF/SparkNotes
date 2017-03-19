# 概念

## 调度中的概念

作业(job)：RDD中由行动操作所生成的一个或者多个调度阶段

调度阶段(stage)：每个作业会因为RDD之间的依赖关系拆分成多组任务集合，也叫作任务集(TaskSet)。调度阶段的划分是由DAGScheduler来划分的，调度阶段有Shuffke Map Stage和Result Stage两种

任务(Task)：分发到Executor上的工作任务，是Spark实际执行应用的最小单元

DAGScheduler：面向调度阶段的任务调度器，负责接收Spark应用提交的作业，根据RDD的依赖关系划分调度阶段，并提交调度阶段给TaskScheduler

TaskScheduler：面向任务的调度器，它接收DAGScheduler提交过来的调度阶段，然后把任务分发到Work节点运行，Worker节点的Executor来运行该任务
