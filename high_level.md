# High level

> Distributed programming is the art of solving the same problem that you can solve on a single computer using multiple computers.


计算机两大任务

- 存储
- 计算


目标

- Scalability
- Performance (and latency)
  - Short response time/low latency for a given piece of work
  - High throughput (rate of processing work)
  - Low utilization of computing resource(s)
- Availability (and fault tolerance)
  - Availability = uptime / (uptime + downtime).
 

Abstractions and models

- System model (asynchronous / synchronous)
- Failure model (crash-fail, partitions, Byzantine)
- Consistency model (strong, eventual)

Design techniques: partition and replicate

![](http://book.mixu.net/distsys/images/part-repl.png)

