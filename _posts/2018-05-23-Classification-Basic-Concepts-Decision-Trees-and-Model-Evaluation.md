---
layout: post
title: Classification - Basic Concepts, Decision Trees, and Model Evaluation
tags: 
  - Data Mining
lang: en
mathjax: true
mathjax_autoNumber: true
---


# Preliminaries
## What tasks classification is the most suited for
Classification techniques are most suited for predicting or describing data sets with binary or nominal categories. They are less effective for ordinal categories (e.g., to classify a person as a member of high-, medium-, or low-income group) **because they do not consider the implicit order among the categories**.
Others forms of relationships, such as the subclass-superclass relationships among categories (e.g. humans and apes are primates, which in turn, is a subclass of mammals) are also ignored.
# Decision tree induction
## Design issues of decision tree induction
There are two key issues to address for a learning algorithm for inducing decision trees:
 1. **How should the training records be split?** Each recursive step of the tree-growing process must select an attribute test condition to divide the records into smaller subsets. To implement this step, the algorithm must provide a method for specifying the test condition for different attribute types as well as an objective measure for evaluating the goodness of each test condition.
 2. **How should the splitting procedure stop?** A stopping condition is needed to terminate the tree-growing process. A possible strategy is to continue expanding a node until either all the records belong to the same class or all the records have identical attribute values. Although both conditions are sufficient to stop any decision tree induction algorithm, other criteria can be imposed to allow the tree growing procedure to terminate earlier.
## Methods for expressing attribute test conditions
### Binary attributes
The test condition for a binary attribute generates two potential outcomes.
### Nominal attributes
Two ways of expressing nominal attributes:
 1. For a multiway split, the number of outcomes depends on the number of distinct values for the corresponding attribute. E.g., [{Single} | {Married} | {Divorced}].
 2. Some decision tree algorithms, such as CART, produce only binary splits by considering all $2^{k-1} - 1$ ways of creating a binary partition of k attribute values. E.g., [{Married} | {Single, Divorced}].
### Ordinal attributes
Ordinal attributes can also produce binary or multiway splits. Ordinal attribute values can be grouped as long as the grouping does not violate the order property of the attribute values. E.g., [{Small, Medium} | {Large, Extra Large}] is acceptable, while [{Small, Large} | {Medium, Extra Large}] not.
### Continuous attributes
For continuous attributes, the test condition can be expressed as a comparison test ($A \lt v$) or ($A \ge v$) with binary outcomes, or a range query with outcomes of the form $v_{i} \le A \lt v_{i+1}$, for i = 1, ..., k.
For the binary case, the decision tree algorithm must consider all possible split positions v, and it selects the one that produces the best partition.
For the multiway split, the algorithm must consider all possible ranges of continuous values. One approach is to apply discretization strategies. After discretization, a new ordinal value will be assigned to each descretized interval. Adjacent intervals can also be aggregated into wider ranges as long as the order property is preserved.
## Measures for selecting the best split
### Entropy
$$Entropy(t) = -\sum_{i=0}^{c-1} p(i|t)log_2 p(i|t)$$

*where c is the number of classes and $0log_2 0 = 0$ in entropy calculation.*
### Gini
Gini(t) = $1 - \sum_{i=0}^{c-1}[p(i|t)]^2$
### Classification error
Classification Error(t) = $1 - \max_{i}{[p(i|t)]}$
### Infomation gain

### Gain ratio




## Algorithm for decision tree induction
## Characteristics of decision tree induction


# Model overfitting
## Overfitting due to presence of noise
## Overfitting due to lack of representative samples
## Overfitting and the multiple comparison procedure




# Estimation of generalization error
## Using resubstitution error
## Incorporating model complexity
### Occam's Razor / principle of parsimony
### Pessimistic error estimate
### Munimum description length principle
### Estimating statistical bounds
### Using a validation bounds


# Handling overfitting in decision tree induction
## Prepruning (early stopping rule)
## Post-pruning

# Evaluating the performance of a classifier
## Holdout method
## Random sampling
## Cross validation
## Bootstrap


# Methods for comparing classifiers
## Estimating a confidence interval for accuracy
## Comparing the performance of two models
## Comparing the performance of two classifiers

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxNTU5NDA3OV19
-->
