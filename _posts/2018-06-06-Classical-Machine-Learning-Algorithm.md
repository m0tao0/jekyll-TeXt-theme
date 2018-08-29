---
layout: post
title: Classic Machine Learning Algorithm
tags: 
  - Classic Machine Learning
lang: en
mathjax: true
mathjax_autoNumber: true
chart: true
---
# 监督学习
## k-近邻算法
#### 优点
 - 训练时间极少；
 - 能够应对多分类任务；
 - 对异常值不敏感；
 - 无数据输入假定。

#### 缺点
 - 计算复杂度高/预测测试样本的成本高；
 - 对skewed distribution敏感，预测结果易倾向于占多数的分类；
 - 高维度数据时，预测准确性会大幅下降，因为较近和较远的点所计算出来的与测试点的距离近似相等；

#### 对未知类别属性的数据集中的每个点归类伪代码
1. 计算已知类别数据集中的点与当前点之间的距离；
2. 按照距离递增次序排序；
3. 选取与当前点距离最小的k个点；
4. 确定前k个点所在类别的出现频率；
5. 返回前k个点出现频率最高的类别作为当前点的预测分类。

#### k的选择
当k值很小时，模型预测的参考范围（即离测试点最近的点的数量）很有限，这就使得模型对（训练）数据集的整体分布重视度较低。较小的k值使得模型的bias更低，但variance变高，或者说决策边界更为曲折。

![](https://raw.githubusercontent.com/m0tao0/m0tao0.github.io/master/images/1nearestneigh.png)

当k至很大时，模型预测是会参考更多的点取平均值，因此受到异常值的影响也会降低。较大的k值使得模型的bias更高，但variance变低，或者说决策边界更为平滑。

![](https://raw.githubusercontent.com/m0tao0/m0tao0.github.io/master/images/20nearestneigh.png)

#### 距离计算方式
通常选择欧几里得距离，但在某些情况下会选择曼哈顿距离（Manhattan distance）, Chebyshev and Hamming distance。

#### 归一化处理
为防止数据某些维度因数值较大而在距离计算产生过大的影响，比如“年龄”和“年收入”同样作为特征时距离的计算可能主要受到“年收入”数值的影响，需要对数据进行归一化处理。

$new\Value=\frac {old\Value - min} {max-min}$

#### 有助于提高模型表现的几种方法
1. 采用加权投票方式。在k个近邻点中，每个点乘以一个加权值，该加权值的大小与该点距离测试点的距离成反比。这样即可保证距离测试点越近的点对预测结果的影响越大。
2. 根据模型的不同应用调整距离测量方式，如Hamming distance用于文本分析。
3. 数据标准化（scikit-learn中的Normalize()会很有帮助）。
4. 降维处理，例如在kNN中使用PCA可以使距离计算更有意义。
5. 使用k-d tree等类近邻算法来储存训练结果以降低预测时间，但这些方法在高维度（20+）时表现很差。在高维度情况下，可考虑使用LHS（locality sensitive hashing）技术。

#### 参考资源
1. [A Complete Guide to K-Nearest-Neighbors with Applications in Python and R](https://kevinzakka.github.io/2016/07/13/k-nearest-neighbor/#more-on-k)
2. [Understanding the Bias-Variance Tradeoff](http://scott.fortmann-roe.com/docs/BiasVariance.html)

## 逻辑回归

#### 优点


#### 缺点



# 无监督学习


## K-means




