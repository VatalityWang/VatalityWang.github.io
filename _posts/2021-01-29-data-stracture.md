---
layout: post
title: data stracture
categories: 学习
description: note
keywords: 散列表
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>





# 散列表

### 定义

实现字典操作的一种有效数据结构。用一个长度与实际存储的关键字数目成比例的数组来存储元素。不把关键字作为下标，而是根据关键字计算出下标。

### 冲突解决

#### 链接法解决冲突

![散列表](/images/blog/散列表.png)

* 双向链表加快插入和删除，最坏情况下都是O(1);
* 给定一个能存放n个元素的，具有m个槽位的散列表T,装载因子$\alpha$=n/m。
* 简单均匀散列假设下，链接法解决冲突，不成功和成功查找平均时间都为$\theta(1+\alpha)$.
* 如果散列表中槽数和元素个数成正比，则$n=\theta(m)$,$\alpha=n/m=O(m)/m=O(1)$,从而查找操作平均需要常数时间。

### 散列函数h(k)

#### 什么是好的散列函数

近似满足均匀假设，每个关键字被等可能散列到m个槽位中。

#### 常用散列函数

* 除法散列

  h(k)=k*mod*m

  m一般取不太接近2的整数幂的素数。

* 乘法散列

  

