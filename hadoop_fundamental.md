# Hadoop Fundamental

## HDFS

![](https://hadoop.apache.org/docs/r1.2.1/images/hdfsarchitecture.gif)

Block size 设置大点减小seek time

Namenodes 不持久化保存 block 位置，在启动的时候从datanode获取

Namenode 单点问题
- namenode 异步原子写状态到本地或远程存储上
- secondary namenode

Block cache
- Managed by namenode
- Configurable on a per-file basis

![Architecture](https://hadoop.apache.org/docs/r2.4.1/hadoop-project-dist/hadoop-hdfs/images/caching.png)

Namenode federation
- Multi namespace multi namenodes
![](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/images/federation.gif)

HDFS HA
- NFS filer
- QJM

Failover and fencing
- failover controller (default zookeeper)
- fencing QJM only allow one namenode to write to the edit log at one time
- client dns map

Read/Write

![](http://ww3.sinaimg.cn/large/7cc66542jw1f0f2kxusx9j20sj0hvgp3.jpg)
![](http://ww4.sinaimg.cn/large/7cc66542jw1f0f2k6mp4hj20sh0jradz.jpg)

## YARN
![](http://ww1.sinaimg.cn/large/7cc66542jw1f0f82u71fvj20sl0b0gn6.jpg)

![](http://ww2.sinaimg.cn/large/7cc66542jw1f0f85nau2xj20k50jbq5k.jpg)

- ResourceManager
- ApplicationMaster
- Resource Model
    - Resource name
    - Amount of memory
    - CPUs
    - Eventually resources such as disk/network I/O, GPUs, and more





## Hadoop I/O

### Data Integrity
CRC-32 循环检测

### Compression
Native lib
CodecPool

### Serialization
Writable Interface


## MapReduce
- MRUnit
- Web UI
- Debug (Remote)
- Log
- Tuning a Job, Profile
- Workflow

How work
- Job Submission
- Job initialization
- Ubertask for small application
- Task assignment
- Task execution
- Progress and Status Updates

![Phases of a Hadoop job](图片 1.png)

FileInputFormat
splits max(minimumSize, min(maximumsize, blockSize)
small files CombineFileInputFormat

日志收集系统
![](http://dongxicheng.org/wp-content/uploads/2011/06/log-system-comapration.jpg)