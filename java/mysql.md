
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

