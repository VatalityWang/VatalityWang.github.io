---
layout: post
title: algorithm summery
categories: 学习
description: note
keywords: divide and conquer
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





# 分治

## 思想定义

* 原问题可分解为几个规模较小，但类似于原问题的子问题。
* 递归地求解这些子问题。
* 合并子问题的解得到原问题的解。

## 举例

### 归并排序

* 分解待排序的n个元素为各有n/2个元素的两个子序列。
* 使用归并排序递归地排序两个子序列。
* 合并两个已排序的子序列产生最终的排序。

```c++
#include<vector>


```

