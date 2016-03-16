# Draft
## Replication


### 分类
Two basic replication approaches
* Synchronous replication
* Asynchronous replication

根据是否会产生分歧分为
* single copy systems  
  * 副本间保持一致性，只有一个副本是活跃的
  * 常见算法
    * 1n messages (asynchronous primary/backup)
    * 2n messages (synchronous primary/backup)
    * 4n messages (2-phase commit, Multi-Paxos)
    * 6n messages (3-phase commit, Paxos with repeated leader election) 
* multi-master systems

![一致性算法比较图](http://book.mixu.net/distsys/images/google-transact09.png)

### Primary/backup replication

* asynchronous primary/backup replication 
  * MySQL, MongoDB
* synchronous primary/backup replication

### Two phase commit (2PC)
MySQL Cluster provides synchronous replication using 2PC

### Partition tolerant consensus algorithms
- Paxox
- Raft

网络分区，Majority decisions