title:  R中的聚类方法
description: Hierarchical Clustering，Partitioning Clustering，Model-Based Clustering
mathjax: true
date: 2015-07-17
tags:  [R,数据挖掘]
categories:  [数据挖掘]

----------------------
# Hierarchical Clustering
## hclust
* hclust
* cutree
 函数原型：cutree(tree, k = NULL, h = NULL) 
 其中k是聚类个数，h是数值类型。h是生成的树的高度的一个cut点。h和k的对应关系如下：
 ```r
    k <- nrow(tree$merge) + 2L - apply(outer(c(tree$height, Inf), h, ">"),2, which.max)
 ```
 等价于：
 ```r
    k <- nrow(treec$merge) + 2L - which.max(c(tree$height, Inf)>hy)
 ```
# Partitioning Clustering

<!-- more -->

# Model-Based Clustering

# 参考文献
[1]: [CRAN Task View: Cluster Analysis & Finite Mixture Models](https://cran.r-project.org/web/views/Cluster.html)
[2]: [Cluster Analysis](http://www.statmethods.net/advstats/cluster.html)