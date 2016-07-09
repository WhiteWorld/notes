# Spark

## 书

[Mastering Apache Spark](https://www.gitbook.com/book/jaceklaskowski/mastering-apache-spark/details)

## 公开课
[BerkeleyX: CS105x Introduction to Apache Spark](https://courses.edx.org/courses/course-v1:BerkeleyX+CS105x+1T2016/info)

## RDD 实现

只读、分区记录的集合

基本属性

 - A list of partitions
 - A function for computing each split
 - A list of dependencies on other RDDs
 - Optionally, a Partitioner for key-value RDDs (e.g. to say that the RDD is hash-partitioned)
 - Optionally, a list of preferred locations to compute each split on (e.g. block locations for an HDFS file)
 
创建

- scala 集合
- 外部数据集

RDD 操作

- 转换 transformation
- 动作 action

RDD 缓存

DISK  MEMORY 

persist()
cache()

窄依赖

宽依赖
