---
layout: post
title: Classification - Basic Concepts, Decision Trees, and Model Evaluation
tags: 
  - Data Mining
lang: en
mathjax: true
mathjax_autoNumber: true
---
## Preliminaries
### What tasks classification is the most suited for
Classification techniques are most suited for predicting or describing data sets with binary or nominal categories. They are less effective for ordinal categories (e.g., to classify a person as a member of high-, medium-, or low-income group) **because they do not consider the implicit order among the categories**.
Others forms of relationships, such as the subclass-superclass relationships among categories (e.g. humans and apes are primates, which in turn, is a subclass of mammals) are also ignored.
## Decision tree induction
### Design issues of decision tree induction
There are two key issues to address for a learning algorithm for inducing decision trees:

1. **How should the training records be split?** Each recursive step of the tree-growing process must select an attribute test condition to divide the records into smaller subsets. To implement this step, the algorithm must provide a method for specifying the test condition for different attribute types as well as an objective measure for evaluating the goodness of each test condition.

2. **How should the splitting procedure stop?** A stopping condition is needed to terminate the tree-growing process. A possible strategy is to continue expanding a node until either all the records belong to the same class or all the records have identical attribute values. Although both conditions are sufficient to stop any decision tree induction algorithm, other criteria can be imposed to allow the tree growing procedure to terminate earlier.

### Methods for expressing attribute test conditions
#### Binary attributes
The test condition for a binary attribute generates two potential outcomes.
#### Nominal attributes
Two ways of expressing nominal attributes:

1. For a multiway split, the number of outcomes depends on the number of distinct values for the corresponding attribute. E.g., ((Single), (Married, Divorced)).

2. Some decision tree algorithms, such as CART, produce only binary splits by considering all $2^{k-1} - 1$ ways of creating a binary partition of k attribute values. E.g., ((Married), (Single, Divorced)).

#### Ordinal attributes
Ordinal attributes can also produce binary or multiway splits. Ordinal attribute values can be grouped as long as the grouping does not violate the order property of the attribute values. E.g., ((Small, Medium), (Large, Extra Large)) is acceptable, while ((Small, Large), (Medium, Extra Large)) not.
#### Continuous attributes
For continuous attributes, the test condition can be expressed as a comparison test ($A \lt v$) or ($A \ge v$) with binary outcomes, or a range query with outcomes of the form $v_{i} \le A \lt v_{i+1}$, for i = 1, ..., k.
For the binary case, the decision tree algorithm must consider all possible split positions v, and it selects the one that produces the best partition.
For the multiway split, the algorithm must consider all possible ranges of continuous values. One approach is to apply discretization strategies. After discretization, a new ordinal value will be assigned to each descretized interval. Adjacent intervals can also be aggregated into wider ranges as long as the order property is preserved.
### Measures for selecting the best split

#### Entropy (at node $t$)
Entropy(t) = $-\sum_{i=0}^{c-1} p(i|t)log_2 p(i|t)$

*where c is the number of classes and $0log_2 0 = 0$ in entropy calculation.*

#### Gini
Gini(t) = $1 - \sum_{i=0}^{c-1}[p(i|t)]^2$
#### Classification error
Classification Error(t) = $1 - \max_{i}{[p(i|t)]}$
#### Information gain
$\Delta =  I(parent) - \sum_{j=1}^{k}\frac {N_{(v_j)}}{N}I_{(v_j)}$

where $I(*)$ is the impurity measure of a given node, $N$ is the total number of records at the parent node, $k$ is the number of attribute values, and $N_{(v_j)}$ is the number of records associated with the child node, $v_j$.

Decision tree induction algorithms often choose a test condition that maximizes the gain $\Delta$. Since $I(parent)$ is the same for all test conditions, maximizing the gain is equivalent to **minimizing the weighted average impurity measures of the child nodes**. Finally, when entropy is used as the impurity measure, the difference in entropy is known as the information gain, $\Delta_{info}$.

#### Gain ratio

Gain ratio =$\frac {\Delta_{info}} {Split Info}$

Here, $Split Info$ = $=\sum_{i=1}^{k}P(v_i)log_2 P(v_i)$ and $k$ is the total number of splits.

### Algorithm for decision tree induction



### Characteristics of decision tree induction

1. Decision tree induction does not require any prior assumptions regarding the type of probability distributions satisfied by the class and other attributes.
2. Decision tree algorithms are quite robust to the presence of noise, especially when methods for avoiding overfitting.
3. The presence of redundant attributes does not adversely affect the accuracy of decision trees.
4. Decision tree induction may encounter the problem of **data fragmentation**, as the number of records becomes smaller as we traverse down the tree. One possible solution is to disallow further splitting when the number of records falls below a certain threshold.
5. **Subtree replication problem**. Since most of the decision tree algorithms use a divide-and-conquer partitioning strategy, the same test  condition can be applied to different parts of the attribute space, leading to the subtree replication problem.
6. The decision boundary of one-attribute test condition is rectilinear. This limits the expressiveness of the decision tree representation for modelling complex relationships among continuous attributes. An **oblique decision tree** ($x + y \lt 1$) can be used to overcome this limitation because it allows test conditions that involve more than one attribute; although such techniques are more expressive and can produce more compact trees, finding the optimal test condition for a given node can be computationally expensive. **Constructive induction** provides another way to partition the data into homogeneous, nonrectangular regions.
7. Studies have shown that **the choice of impurity measure has little effect on the performance of decision tree induction algorithms**. In contrast, the strategy used to prune the tree has a greater impact on the final tree than the choice of impurity measure.


## Model overfitting
### Overfitting due to presence of noise

Model overffting may arise when algorithm tries to fit to noise (e.g. mislabeled training data) in the training set.

### Overfitting due to lack of representative samples

Models that make their classification decisions based on a small number of training records are also susceptible to overfitting. Such models can be generated because of lack of representative samples in the training data and learning algorithms that continue to refine their models even when few training records are available.

### Overfitting and the multiple comparison procedure

Model overfitting may arise in learning algorithms that employ a methodology known as multiple comparison procedure.


## Estimation of generalization error
### Using resubstitution error

The resubstitution estimate approach assumes that the training set is a good representation of the overall data. However, this is usually not the case.

### Incorporating model complexity
#### Occam's Razor / principle of parsimony

> Given two models with the same generalization errors, the simpler model is preferred over the more complex model.

Occam's razor is intuitive because the additional components in a complex model stand a greater chance of being fitted purely by chance.

> Everything should be made as simple as possible, but not simpler.
>
> -- Albert Einstein

#### Pessimistic error estimate

$e_g(T)$ = $\frac {\sum_{i=1}^{k}[e(t_i)+{\Omega(t_i)}]}{\sum_{i=1}^{k}n(t_i)}$ = $\frac{e(T)+\Omega(T)}{N_t}$

*where $k$ is the number of lead nodes, $e(T)$ is the overall training error of the decision tree, $N_t$ is the number of training records, and $\Omega(t_i)$ is the penalty term associated with each node $t_i$.*

#### Munimum description length principle

Another way to incorporate model complexity is based on information-theoretic approach know as the minimum description length or MDL principle.

#### Estimating statistical bounds

The generalization error can also be estimated as a statistical correction to the training error. Since generalization error tends to be larger than training error, the statistical correction is usually computed as an upper bound to the training error, taking into account the number of training records that reach a particular leaf node.

#### Using a validation set

The original training data is divided into two smaller subsets, of which one is used for training and the other estimating the generalization error.


## Handling overfitting in decision tree induction
### Prepruning (early stopping rule)

The tree-growing algorithm is halted before generating a fully grown tree that perfectly fits the entire training data. To do this, a more restrictive stopping condition must be used; e.g., stop expanding a leaf node when the observed gain in impurity measure (or improvement in the estimated generalization error) falls below a certain threshold.

- Pros: it avoids generating overly complex subtrees that overfit the training data.
- Cons: it is difficult to choose the right threshold for early termination. Too high of a threshold will result in underfitted models, while a threshold that is set too low may not be sufficient to overcome the model overfitting problem. Furthermore, even if no significant gain is obtained using one of the existing attribute test conditions, subsequent splitting may result in better subtrees.

### Post-pruning

The decision tree is initially grown to its maximum size. This is followed by a tree-pruning step, which proceeds to trim the fully grown tree in a bottom-up fashion. Trimming can be done by replacing a subtree with:

1. a new leaf node whose class label is determined from the majority class of records affiliated with the subtree;
2. or, the most frequently used branch of the subtree

The tree-pruning step terminates when no further improvement is observed. Post-pruning tends to give better results than prepruning because it makes pruning decisions based on a fully grown tree, unlike prepruning, which can suffer from premature termination of the tree-growing process. However, for post-pruning, the additional computations needed to grow the full tree may be wasted when the subtree is pruned.

## Evaluating the performance of a classifier
### Holdout method

Holdout method is to partition data into two disjoint sets, i.e. training and test sets. This method has some limitations:

1. Fewer labeled examples are available for training, so the model may not be as good as when all the labeled examples are used for training.
2. Smaller training set size leads to larger variance, while larger size leads to less reliable estimated accuracy computed from the smaller test set.
3. Actually, training and testing set are no longer independent of each other.

### Random sampling

The holdout method can be repeated several times to improve the estimation of a classifier's performance, and this method is known as random subsampling.

$acc_{sub}=\sum_{i=1}^{k}acc_i/k$

*where $acc_i$ is the model accuracy during the $i^{th}$ iteration.*

This method also has the limitations of holdout method; besides, it has no control over the number of times each record is used for testing and training. Consequently, some records might be used for training more often than others.

### Cross validation (k-fold)

This is an alternative to random sampling and split the dataset into k folds; then, each fold will be used as a validation/test set when the others are being used for training. The total error is found by summing up the errors for all k runs.

- Pros: this method utilizes as much data as possible for training.
- Cons: it is computationally expensive to repeat the procedure when k is large (e.g., when k is equal to the total number of records). When the value of k is increasing, the variance of the estimated performance metric tends to be high (as the model will have much more but smaller-sized testing set).

### Bootstrap

In the bootstrap approach, the training records are sampled with replacement; i.e., a record already chosen for training is put back into the original pool of records so that it is equally likely to be redrawn. One of the more widely used approaches is the **.632 bootstrap**, which computes the overall accuracy by combining the accuracies of each bootstrap sample $\epsilon_i$ with the accuracy computed from a training set that contains all the labeled examples in the original data $acc_s$:

Accuracy, $acc_boot=\frac{1}{b}\sum_{i=1}^b(0.632\epsilon_i+0.368acc_s)$

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxNTU5NDA3OV19
-->
