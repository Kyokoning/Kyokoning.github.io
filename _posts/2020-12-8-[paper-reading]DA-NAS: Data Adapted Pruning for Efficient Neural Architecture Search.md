---
layout:     post
title:      "[paper-reading]DA-NAS: Data Adapted Pruning for Efficient Neural Architecture Search"
subtitle:   ""
date:       2020-12-8 16:40:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - gradient-based leanring
    - NAS
    - paper reading
---

[TOC]

ECCV2020

### 摘要
Gradient-based
如何快速搜索网络？一个方法是在小的proxy dataset上搜索，然后将网络转移到大的dataset上，但是这没法保证网络在目标数据集上最优；另一个方法是降低搜索空间大小，但是这有违背NAS的初衷。

本文提出了DA-NAS，可以直接在大型数据集上搜索大的搜索空间。

我们设计了一个渐进式数据适应修剪策略（Progressive data adapted pruning strategy)，它会将dataset中不那么有效率的子集逐渐剔除（例如比较简单的类别），然后找到数据集中最佳的子集。

本文使用参数搜索空间（应该就是gradient-based）。在ImageNet上的实验证明，他比之前的方法快两倍，accuracy有76.2%.

### 1. Introduction

本文的灵感来自于观察结果：在分类任务中，简单的类别在训练的时候容易使模型快速瘦脸，但困难的类别则需要更多的时间。

因此本文提出的方法：在训练开始的时候使用目标数据集的子集（简单的类别），然后修剪搜索空间。随着搜索空间被精简，训练数据集也逐渐完整。

贡献：
1. DA-NAS是第一个在dataset scheduling和block pruning之间建立连接的算法。
2. 本文提出了渐进式的block-level的剪枝方法，according to data adaption（就是随着训练数据集从小到大，逐渐在block-level剪枝训练空间）
3. DA-NAS在多个领域使用。本文还在姿态识别领域使用了。

### 3. 本文方法的实验依据
三个实验结果：

1. 对于分类任务，有些class的训练很简单，有些class训练比较困难：

   ![image-20201210201952700](/Users/xnchen/Library/Application Support/typora-user-images/image-20201210201952700.png)

可视化为随着training时迭代epoch的增加，accuracy的进展情况。
根据矩阵的行方差对矩阵进行排序。可以发现在上面的是easy的，下面的是hard的。

2. 识别简单class的神经元在训练开始的时候很快收敛，并且在之后的epoch中保持稳定。识别困难class的神经元需要更多的时间进行训练。

![image-20201210202009143](/Users/xnchen/Library/Application Support/typora-user-images/image-20201210202009143.png)

上图的纵坐标是从easy到hard的class的训练之后的神经元和结果的相关性。其中行排序和1.中相同，横坐标是根据相关性最大值进行排序的结果。可以发现所有的神经元在训练中都应该发挥作用。（所以要怎么剪枝？

3. 不同架构的网络对于分类任务中class的easy和hard的认知是相同的。

### 4.DA-NAS(Data Adapted NAS)

#### 如何区分easy和hard的class？

没看懂

#### 扩展的搜索空间

本文使用的搜索空间的operation和operation参数都远远多于前人

![image-20201210202027505](/Users/xnchen/Library/Application Support/typora-user-images/image-20201210202027505.png)

![image-20201210202038140](/Users/xnchen/Library/Application Support/typora-user-images/image-20201210202038140.png)

#### cost constraints

在Lossfunction中加入FLOPs or 硬件latency的cost constraints。

#### 训练策略

本文idea的亮点。

![image-20201210202049630](/Users/xnchen/Library/Application Support/typora-user-images/image-20201210202049630.png)

在本文实际训练过程中，使用4个V100GPu。supernet的warmup进行了10个epoch，接下来进行三个step的搜索，每个step含有20个epoch。这些step分别使用100、300、600、1000个class进行训练。剪枝使用的pruning ratio为0.4（可是到底怎么用）


