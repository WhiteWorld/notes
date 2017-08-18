
连接 MySQL 方式

- TCP/IP
- 命名管道和共享内存
- UNIX 域套接字

InnoDB 体系结构

- 后台线程
    - Master Thread
    - IO Thread
    - Purge Thread
    - Page Cleaner Thread
- 内存
    - 缓冲池
        - 数据页
        - 索引页
        - 插入缓冲
        - 自适应哈希索引
        - 锁信息
        - 数据字典信息
    - LRU List、Free List 和 Flush List
    - 重做日志缓冲
    - 额外内存池

CheckPoint 

- Sharp CheckPoint 数据库关闭时刷新脏页到磁盘
- Fuzzy CheckPoint 刷新一部分脏页到磁盘
    - Master Thread CheckPoint
    - FLUSH_LRU_LIST CheckPoint
    - Async/Sync Flush CheckPoint
    - Dirty Page too much CheckPoint

Master Thread

- loop 、backgroup loop 、flush loop 、suspend loop

InnoDB 关键特性

- 插入缓冲
- 两次写
- 自适应哈希索引
- 异步 IO
- 刷新邻接页