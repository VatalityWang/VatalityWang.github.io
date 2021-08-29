---
layout: post
title: few shot learning
categories: 学习
description: 总结
keywords: 小样本
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

# 1 论文总体情况

![image-20201223071902751](/images/blog/image-20201223071902751.png)

| MetaGan         | 促使学习更好的决策边界                                       |
| --------------- | ------------------------------------------------------------ |
| RelationNet     | 两个网络 ，一个学习特征隐射，一个比较特征                    |
| PrototypicalNet | 一个网络，一个隐射特征，用距离度量函数来分类                 |
| MatchNet        | Calculate "attention" as softmax over support-query distances |



# 2 代码连接

* relation-network

  https://github.com/floodsung/LearningToCompare_FSL

* MAML,Match-network,relation-network

  https://github.com/oscarknagg/few-shot

# 3 实验仿真

## 3.1 仿真数据+ Prototypical Network 6-way 1-shot

![image-20201224105127197](/images/blog/image-20201224105127197.png)

## 3.2 仿真数据+AlexNet

![image-20201224105829006](/images/blog/image-20201224105829006.png)