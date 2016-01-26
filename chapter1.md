# HBase


## Secondary Index
- Filter Query (client)
- Periodic-Update Secondary Index (MR job update another table)

## RowKey design

    根据使用场景设计
    
## RegionServer Splitting

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