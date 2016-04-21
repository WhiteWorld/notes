# Mathematics

## Linear Algebra

参考：[麻省理工公开课：线性代数](http://open.163.com/special/opencourse/daishu.html)
相关笔记：
http://blog.csdn.net/suqier1314520/article/category/1571247
http://blog.csdn.net/xdfyoga1/article/category/2315349

### 线性方程组的几何解释
row picture
![](http://img.blog.csdn.net/20140608134044718?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGRmeW9nYTE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
行表示的直线的交点为方程的解。

column picture
![](http://img.blog.csdn.net/20140608135024343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGRmeW9nYTE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
列表示的向量通过怎样的线性组合得到一个向量。

有一个很重要的问题，对于任意b，是否都能求解Ax=b，用列的角度看待方程，这个问题即列的线性组合是否能覆盖整个空间?很明显这跟A矩阵有很大的关系，如果A是非奇异阵，这样才能组合出所有的b，以一个三方程三未知数的方程组来理解，如果系数矩阵A的3个列向量在一个平面上，那么由他们组合出的所有向量都在那个平面上，在那个平面之外的所有b都是无法得到的,这就造成方程无解。

矩阵与向量相乘的方法

- 将矩阵A与向量x的相乘，看着A各列的线性组合，这是极力推荐的。
- 原始点乘方式。

### 矩阵消元



乘法和匿矩阵
乘法：四种算法
匿矩阵：是否有匿矩阵，两个行向量有夹角