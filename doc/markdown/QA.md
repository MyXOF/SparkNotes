<!-- TOC -->

- [Q&A](#qa)
    - [Q1:为什么Spark里面对数据的操作需要分为transform和action两种？](#q1为什么spark里面对数据的操作需要分为transform和action两种)

<!-- /TOC -->

# Q&A

## Q1:为什么Spark里面对数据的操作需要分为transform和action两种？

transform返回的是一个RDD对象，action返回的是一个非RDD对象。从返回的类型就可以看到，transform操作是对原有数据内容的转化，而action能改变数据存在的形态，像count操作这种，完全改变了数据原有的形态。而且对于transform操作，可以利用惰性求值的方法，将窄依赖一次性计算最终结果，而不像MR那样将每次计算的中间结果写入磁盘，当遇到宽依赖的时候，才按照stage进行划分
