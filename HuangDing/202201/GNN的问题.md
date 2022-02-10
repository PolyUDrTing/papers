# GNN的问题

1）数据集太小，overfitting的问题，在一些数据上training acc为100%的大概率是这个问题，需要通过防止过拟合的技术来解决

 2）vanishing gradient，这是CNN里一样存在的问题，当层数太深导致网络的参数不能得到有效的训练。这个问题可以加skip connections可以有效解决

​	加一个残差项

 3）over smoothing

​	同一个连通分量里的节点会收敛的一个值，一个解决的方法是通过有效地改变图的结构或卷积的领接节点来解决。



# 池化层

池化层其实就是上文中提到的各个aggregator，用来将邻居的Embedding聚合起来生成一个汇总的Embedding再和节点自身的Embedding进行操作。

随机池化的研究比较少。

### AvgPooling

###  SumPooling

### MaxPooling

### SortPooling

### TopKPooling： 主要思路是将节点Embedding隐射到1维空间中选择其中top k个节点再进行图卷积的计算

###  SAGPooling

### GlobalAttentionPooling