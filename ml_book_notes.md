# Book Notes







## 机器学习实战

监督学习: 机器从数据中获取目标变量。目标变量分为两种：离散变量（分类），连续变量（回归）
无监督学习：聚类，输入数据无标签

机器学习程序开发步骤

* 收集数据
* 准备输入数据
* 分析输入数据
* 人工参与
* 训练算法
* 测试算法
* 使用算法

k-近邻算法 kNN

* 优点：简单高效
* 缺点：保存全部数据集，计算需要存储空间大，耗时

为了提高K近邻搜索的效率，可以考虑kd树的方法。

决策树

* 决策树的构造
  * 信息增益
  * 划分数据集
  * 递归构造树
  * 决策树的使用
    * 序列化到磁盘



朴素贝叶斯

条件概率

Logistic 回归

优点：代价不高，易于实现
缺点：容易欠拟合，分类精度可能不高

推到过程：[基于Logistic回归的二元分类应用（含公式推导）](http://www.jianshu.com/p/9ffab4c4f76d)

Softmax 算法：多分类算法，Logistic 回归的一般化

SVM 支持向量机

[支持向量机系列](http://blog.pluskid.org/?page_id=683)
[支持向量机SVM](http://www.cnblogs.com/jerrylead/archive/2011/03/13/1982639.html)

线性分类器-&gt;转化为对偶问题并优化求解-&gt;
最大间隔

Adaboost

[ 数据挖掘算法学习（八）Adaboost算法](http://blog.csdn.net/iemyxie/article/details/40423907)

