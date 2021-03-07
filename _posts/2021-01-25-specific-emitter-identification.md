---
layout: post
title: specific emitter identification
categories: 学习
description: paper summary
keywords: signal process
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



# Domain adaption

迁移学习常见问题之一，域不同但任务相同，且源域数据有标签而目标域数据没有标签或者很少标签。





# traditional signal process







# few shot 





# adversarial 

## Discriminative adversarial networks for specific emitter identification  

### 核心思想

* 同一类型的不同个体包含的特征有意调制和无意调制两种。
* 有意调制（IMI）是相同的特征，而无意调制(UMI)特征是不同的。
* 无意调制是指纹特征的来源。
* 提出对抗判别模型DAN，学习UMI和IMI之间清晰的决策边界。从而分离出IMI，减少UMI提取过程中的负担。

![image-20210125205437232](/images/blog/image-20210125205437232.png)

* 圆：两个辐射源个体的共有特征。
* 三角：两个辐射源个体的独有特征。

## 整体网络架构

![image-20210125205925767](/images/blog/image-20210125205925767.png)

* 

