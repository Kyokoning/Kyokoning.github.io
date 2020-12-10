---
layout:     post
title:      "[paper-reading]Progressive Neural Architecture Search"
subtitle:   ""
date:       2020-12-7 16:40:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - reforcement learning
    - NAS
    - paper reading
---

[TOC]

ECCV2018

### 摘要

PNAS
也是Reforcement learning
本文提出了顺序的基于模型的优化策略（Sequential model-based optimization strategy）。这种方法按照复杂度递增的顺序搜索结构。
同时学习一个代理模型（Surrogate model）预测candidate model的performance以此来减少训练模型的数量。
本方法比Zoph在2018年的RL方法的论文搜索效率搞5倍，总计算速度高8倍。本文的方法搜索到的结构在CIFAR-10和ImageNet上都能获得state-of-art精确度

### 1. Introduction

1. 本文继承自[Learning transferable architectures for scalable image recognition.](https://app.yinxiang.com/shard/s50/nl/12523011/fe43c404-c188-414f-ae25-2b2445bc0e4f/)
2. 在搜索固定的cell的基础上，本文从浅至深搜索网络结构。cell内block随着搜索迭代次数增加而增加。
3. 提出了代理模型/函数（Surrogate model/function）。将结构输入该模型/函数，将会输出一预测performance。
4. 本文的方法大大加快了搜索时间（五倍效率），整体计算降低八倍。在CIFAR-10和ImageNet上得到了state-of-art结果。

### 3. 搜索空间

和[41](https://app.yinxiang.com/shard/s50/nl/12523011/fe43c404-c188-414f-ae25-2b2445bc0e4f/)基本相同，减少了在[41]中没有使用的operation和combination operation选项使搜索空间变小，并且去除了Reduction cell的搜索，单纯用normal cell改成2stride来形成reduction cell。

### 4. Method

#### 4.1 递进式的NAS

算法：

1. 一开始设定一个cell中含有一个block，然后在candidate set中把所有可能的1block cell都放进去。
2. 训练candidate set中所有的cell，得到的Accuracy用于训练一个predictor（cell structure→accuracy的predictor）。
3. 往每个candidate set中的cell加一个block，得到candidate set全是2block cell。将这些candidate送入predictor中，得到预测的top-K accuracy candidate。
4. 将top-K保留在candidate set中，进行训练。得到的accuracy继续训练predictor
5. 循环直到cell中block达到B个

#### 4.2 predictor

用于预测模型精确度的predictor需要具有①可接受长度可变的cell structure描述；②输出不需要是结构的确切精确度，但是输出结果的排序得是正确的；③训练predictor需要有效率，因为数据不多。

本文使用了两种predictor实现方法：
- LSTM：使用LSTM接收长度可变的structure描述，总共要有4×b个LSTM block，b是候选cell内含有的block数量，4是输入×2、operation×2。LSTM block输入是一组代表选择的one-hot编码vector。
- MLP（多层感知器）：输入长度得是固定的。本文的编码方式是：使用D维one-hot vector表示一个选择，那么一个cell内block就是4D维vector，将所有cell内block平均起来。

predictor的训练：
因为输入数据少，使用五个predictor，每个predictor都从scratch开始训练，每次训练使用当轮中4/5的数据。（感觉就是bagging方法）。每次使用SGD训练几个step。

