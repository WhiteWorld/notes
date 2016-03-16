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

网络分区，Majority decisions （ (N/2 + 1)-of-N）

### Roles
leader follower

### Epochs
During each epoch only one node is the designated leader 

![epoch](http://book.mixu.net/distsys/images/epoch.png)
### Leader changes via duels
所有节点开始都是follower，leader维护心跳，follower通过心跳检测leader的状态和是否发生分区。

当节点检测到leader出问题后，它切换到“candidata”状态，开始一轮选举，竞选leader。

为了成为leader，节点必须接受大多数的投票。简单的投票规则是先来先得。同时增加一个随机的等待时间来解决同时请求选举的问题。

### Numbered proposals within an epoch
During each epoch, the leader proposes one value at a time to be voted upon. Within each epoch, each proposal is numbered with a unique strictly increasing number. The followers (voters / acceptors) accept the first proposal they receive for a particular proposal number.

