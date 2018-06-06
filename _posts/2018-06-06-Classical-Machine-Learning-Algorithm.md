---
layout: post
title: Summary of Classic Machine Learning Algorith
tags: 
  - Classic Machine Learning
lang: en
mathjax: true
mathjax_autoNumber: true
---
## 监督学习
### k-近邻算法
#### 特点
 - 优点：精度高、对异常值不敏感、无数据输入假定。
 - 缺点：计算复杂度高、空间复杂度高。
 - 使用数据范围：数值型和标称型。
#### 对未知类别属性的数据集中的每个点归类伪代码
1. 计算已知类别数据集中的点与当前点之间的距离；
2. 按照距离递增次序排序；
3. 选取与当前点距离最小的k个点；
4. 确定前k个点所在类别的出现频率；
5. 返回前k个点出现频率最高的类别作为当前点的预测分类。

#### k的选择
When K is small, we are restraining the region of a given prediction and forcing our classifier to be “more blind” to the overall distribution. A small value for K provides the most flexible fit, which will have low bias but high variance. Graphically, our decision boundary will be more jagged.
On the other hand, a higher K averages more voters in each prediction and hence is more resilient to outliers. Larger values of K will have smoother decision boundaries which means lower variance but increased bias.

#### 距离计算方式
通常选择欧几里得距离，但在某些情况下会选择the Manhattan, Chebyshev and Hamming distance.

数据归一化
$newValue=\frac {oldValue - min} {max-min}$

Pros：训练时间极少；能够应对多分类任务；对异常值不敏感。
Cons：预测测试样本的成本高；对skewed distribution敏感，预测结果易倾向于占多数的分类；高维度数据时，预测准确性会大幅下降，因为较近和较远的点所计算出来的距离近似相等。





## 无监督学习



