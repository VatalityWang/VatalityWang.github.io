---
layout: post
title: paper reading
categories: 学习
description: note
keywords: small data,few shot
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





# 1 MetaCGAN A Novel GAN Model for Generating high quality and diversity images with few training data

![image-20210117094956295](/images/blog/image-20210117094956295.png)

## 发表

ICJNN A 会,参考[计算机类顶级会议排名+投稿经验](https://www.twblogs.net/a/5b7b02482b7177539c24ae9a/?lang=zh-cn)

## 核心思想		

基于迁移学习，让generator学习到其他类样本的先验信息，迁移到新类上，利用MetaNet生成CGAN反卷积层的权重，以辅助生成质量更高的多样性样本。

## 难点
代码实现。

## 对比

* DCGAN 大量数据   

* WGAN  大量数据

* CGAN  新类少量，旧类大量

## 数据集

* MNIST

  0,1,2,3,4作为训练基本类,5,6,7,8,9作为新类,每类只包含10张图片.

* Fashion MNIST

  t-shirt  trouser  pullover  dress  coat  作为基本类,sandal  shirt  sneaker  bag  ankle  boot  作为新类.

* CelebA

  女人作为基本类,男人作为新类,每类50张

  ## 训练算法

![image-20210117145330833](/images/blog/image-20210117145330833.png)

## Tricks

* 使用instance Batch normalization,参考:[pytorch常用normalization函数](https://www.cnblogs.com/wanghui-garcia/p/10877700.html)

## 评估

* 定性

  对比生成图片的质量

* 定量

  IS(inception score)=$e^{(E_x[D_{KL}(P(y \mid x) \parallel  p(y))])}$

  * x:生成的图像
  * y:训练好的分类器去预测x属于某一个类别的概率所获得的向量
  * p(y):边缘分布
  * $D_{KL}$:kl散度
  * p(y|x)低意味着决策边界很紧凑,p(y)高意味着图像的高度多样性
  * 通常生成图片的多样性可被类之间的决策边界的可区分性所表征.如果两张图片高概率不相似,则应被分为不同的类.

  AMT(Amazon Mechanical Turk )

  * 评估CelebA上生成的图像.

  
# 2 Generative Latent Implicit Conditional Optimization when Learning from Small Sample

![image-20210117150514932](/images/blog/image-20210117150514932.png)

## 发表

ICPR A 会,参考[计算机类顶级会议排名+投稿经验](https://www.twblogs.net/a/5b7b02482b7177539c24ae9a/?lang=zh-cn)

## 核心思想

提出GLICO(Generative Latent Implicit Conditional Optimization),学习一个训练空间到潜在空间的隐射,生成器从潜在空间向量中生成图片.不依赖于大量未标记图片,GLICO只需要小的带标签数据点集.实际上,合成新的图片每类只需要5到10张在总共10类样本中,不需要任何先验信息.最后用提出的方法从潜在空间中利用球面插值采样用生成器生成新的图片,生成的图片可以提升分类精度.

## 问题提出

1 严格的小样本设置,学习者每一类只能访问到小数量样本(通常5~10),类别数也不多.

* 半监督

  学习者学习到大量无标签数据.

* 小样本场景

  学习者可以接触到大量带标签的各个类别数据,只是这些类别的数据不参与当前分类任务.

大多数小样本算法依赖于迁移学习,从大量带标签训练样本中,大多半监督学习算法从无标签数据中迁移知识.



2 大多数针对小数据样本场景设计的方法不能利用外围数据来进行迁移学习,可通过施加强的先验到模型中来解决这个问题,但是在许多场景下由于未知域以及这样的先验知识不可得.

​	数据增强可能会有用,利用

* 有关数据的弱先验,如半监督学习,传导学习.
* 自训练方法
* 生成模型



3 GAN为何不能用?

* 需要大量数据来进行有效训练.
* 小样本场景下表现差.

## 方法解决
​	在潜在空间中进行优化.为每一个数据点分别学习一个潜在空间码.在潜在空间中,让内类样本尽量相互靠拢,类间样本尽量远离.通过一个由已知多标签数据训练的分类器.



## 损失函数

$L_{percep} (x_i,z_i;\theta)=\sum_{j} \lambda_j\parallel \xi_j(G_{\theta}([z_i,\varepsilon]))-\xi_j(x_i)  \parallel _1 $

### 感知损失函数

* $z_i\epsilon Z$ ,$Z$:单位球面,在$R^d$ 空间中,表示隐层空间.
* $x_i \epsilon X \mid  X_i \epsilon R^{3\ast H \ast W}$  ,表示训练集中的样本.
* $G_\theta$:生成器.
* $\xi_j(x_i)$ :卷积网络的输出层.

![image-20210117172632460](/images/blog/image-20210117172632460.png)

### 优化目标

$min_\theta \sum_{i=1}^{n}[min_{z_i\epsilon Z}L_{percep}(x_i,z_i;\theta)]$

### 分类损失







# 3 Domain Adaptation through Synthesis for Unsupervised Person Re-identification

## 发表

ECCV 2018

## 核心思想

提出用基于渲染的合成数据加基于cycle-gan的域迁移来合成新的数据集，用于后续模型微调重识别网络。以实现未知光照条件下的行人重识别。

## 潜在挑战

* 训练合成数据时需要克服合成数据分布和真实数据分布之间的差异。网络可能只学习到合成数据的特征却没有学到真实数据的特征。
* 解决：域适应，合成数据看成源域，真实数据看出目标域
  * 使合成数据更真实。
  * 最小化源域和目标域数据之间的域迁移。
  * 给出合成数据和域转换，产生在目标域的训练数据，用于微调，以提升性能。

## 做法

### 域适应

![image-20210131095757582](/images/blog/image-20210131095757582.png)

* 光照推理
* 域转化
* 微调

选择一张目标域中的无标签图片，通过光照推理从合成域中选择最接近目标域光照的图片，然后把图片通过转化使源域（合成域）中的图片更像目标域中的图片，但是仍然保留了已知的身份信息，用生成的图片来微调重识别网络。



频谱能量分析；

提取出来的深度特征的名字？





