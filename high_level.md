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

A system model

a set of assumptions about the environment and facilities on which a distributed system is implemented

Nodes in our system model

- the ability to execute a program
- the ability to store data into volatile memory (which can be lost upon failure) and into stable state (which can be read after a failure)
- a clock (which may or may not be assumed to be accurate)

FLP

there does not exist a (deterministic) algorithm for the consensus problem in an asynchronous system subject to failures, even if messages can never be lost, at most one process may fail, and it can only fail by crashing (stopping executing)

The CAP theorem

![](http://book.mixu.net/distsys/images/CAP.png)

- Consistency: all nodes see the same data at the same time.
- Availability: node failures do not prevent survivors from continuing to operate.
- Partition tolerance: the system continues to operate despite message loss due to network and/or node failure


