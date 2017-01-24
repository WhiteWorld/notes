白皮书

https://cloud.google.com/blog/big-data/2017/01/learn-tensorflow-and-deep-learning-without-a-phd

### 介绍

第一代 DistBelief

第二代 TensorFlow

### 编程模型和基本概念

计算使用包含一组节点的有向图表示。每个节点有零到多个输入和输出，表示一个操作的实例。操作的属性必须提供或通过infer得出。Kernel 是一个操作的部分实现。客户端程序通过Session和TensorFlow 系统交互。Variables 是一个特别的操作。

### 实现

本地 和 分布式实现。本地：client  master  work 运行在一台机器。分布式：支持client  master work 在不同机器的不同进程。

Tensor 是一个typed，多维数组。

操作 和 核

客户端程序通过Session和系统交互。





安装 pyenv，安装 anaconda

