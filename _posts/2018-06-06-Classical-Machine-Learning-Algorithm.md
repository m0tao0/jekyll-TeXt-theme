
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
 - 通常k是不大于20的整数。
#### 对未知类别属性的数据集中的每个点归类伪代码
1. 计算已知类别数据集中的点与当前点之间的距离；
2. 按照距离递增次序排序；
3. 选取与当前点距离最小的k个点；
4. 确定前k个点所在类别的出现频率；
5. 返回前k个点出现频率最高的类别作为当前点的预测分类。

k的选择
距离计算方式
数据归一化
$newValue=\frac {oldValue - min} {max-min}$

Pros：训练时间极少；能够应对多分类任务；对异常值不敏感
Cons：预测测试样本的成本高；对skewed distribution敏感，预测结果易倾向于占多数的分类；





## 无监督学习



