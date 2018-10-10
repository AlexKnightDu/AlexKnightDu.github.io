---
title: 关于VAE
date: 2018-09-30 10:19:21
tags: [ML, Note]
mathjax: true
---

Autoencoder可以看做一种前向网络的特殊情况，所以可以用相同的训练方法。但是不同于常用的前向网络，Autoencoder还可以通过recirculation来进行训练，即通过比较输入和生成结果的activation的来进行学习。  

#### Undercomplete Autoencoder
对于 Undercomplete Autoencoder，学习过程可以简单地表示为:  
$$L(x,g(f(x)))$$  
其中如果decider是线性并且L是均方误差，那么最终得到的子空间呢与PCA相同。
如果Hidden code具有的维度比输入数据要高，或者Autoencoder过于复杂，则学不到任何有用的信息。

#### Regularized Autoencoder
相比于限制Autoencoder，Re

