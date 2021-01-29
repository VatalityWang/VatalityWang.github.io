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