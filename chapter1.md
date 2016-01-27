# HBase


## Secondary Index
- Filter Query (client)
- Periodic-Update Secondary Index (MR job update another table)

## RowKey design

    根据使用场景设计
    
## RegionServer Splitting

![](https://hbase.apache.org/images/region_split_process.png)

- zookeeper 获取锁
- Master 感知
- 在父Region的HDFS目录下建立.split目录
- 标记父Region下线
- 创建daugherA 和 daugherB和引用文件
- 创建Region目录，移动子Region到目录中
- RegionServer Put 请求到 META 表
- 打开A和B
- 插入A和B的主机信息至META表
- 更新zookeeper为完成
- compaction操作时会逐步删除父region文件，直至移除父region

## WAL
 
  当 RegionServer 在 MemStore flushed 前崩溃或不可用时 replay changes
  
###  MultiWAL
  
  加速 replay，但限于多 region 上
  
### WAL Splitting

edits in the WAL file must be grouped by region so that particular sets can be replayed to regenerate the data in a particular region.

由 HMaster 来完成。在集群启动时或 RegionServer 关闭时进行。

regions affected by log splitting are unavailable until the process completes.

![](http://blog.cloudera.com//wp-content/uploads/2012/06/log-splitting.png)

步骤

- rename 目录，保证新请求可用
- split 到每个 Region 一个文件
- 每个region replay

提升性能：distributed log processing

## Region

### HBase 为少量(20~200)的region设计的

### region assignment

### region 状态机

![](https://hbase.apache.org/images/region_states.png)

## Compaction

Major minor

多种 major 策略

## Bulk Loading

直接生成HFile文件，然后bulk load到HBase 中


## Timeline-consistent

region replica

```
public enum Consistency {
    STRONG,
    TIMELINE
}
```

![](https://hbase.apache.org/images/timeline_consistency.png)


