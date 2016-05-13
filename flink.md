# Flink

## links

[官网](https://flink.apache.org/)
[Flink Traning](http://dataartisans.github.io/flink-training/)

Flink 操作二进制数据

现在很多项目如 Apache Spark， Apache Drill等运行在 JVM 上。如何在在基于 JVM 的数据上对大量数据进行排序、缓存和合并是常见的挑战。

把数据 Objects 直接放入 Heap 可能会导致 OutOfMemoryError 错误，GC 的负载也比较高。

Flink 把序列化的对象保存在一个固定的预分配的内存段里。通过使用DBMS风格的 sort 和 join 算法操作尽可能多的二进制数据，减少序列化和反序列化的压力。如图：
![](https://flink.apache.org/img/blog/memory-mgmt.png)

Flink

TaskManager MemoryManager IOManager 

内存布局
![](https://flink.apache.org/img/blog/memory-alloc.png)


Memory Segment 组织
![](https://flink.apache.org/img/blog/data-serialization.png)

Sort 操作

![](https://flink.apache.org/img/blog/sorting-binary-data-1.png)

![](https://flink.apache.org/img/blog/sorting-binary-data-2.png)
![](https://flink.apache.org/img/blog/sorting-binary-data-3.png)
Flink 的内存管理的优势

- Flink’s active memory management avoids nasty OutOfMemoryErrors that kill your JVMs and reduces garbage collection overhead.
- Flink features a highly efficient data de/serialization stack that facilitates operations on binary data and makes more data fit into memory.
- Flink’s DBMS-style operators operate natively on binary data yielding high performance in-memory and destage gracefully to disk if necessary.

off-heap 的好处

- 大 JVM 操作比较困难，垃圾回收代价昂贵。
- I/O 和 网络效率高，零拷贝
- 缓存的数据不因为进程的crash而丢失

off-heap 缺点

- on-heap 简单，直观
- 临时内存 heap 中比较廉价
- 在 heap 中的操作更快

