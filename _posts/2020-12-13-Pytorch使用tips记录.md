---
layout:     post
title:      "Pytorch使用tips记录"
subtitle:   ""
date:       2020-12-14 15:40:41
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - Pytorch
---

[TOC]

## abstract

一些非常简单的小方法的记录

## 方法

### Torch.numel

```
torch.numel(input) -> int
torch.nelement(input) -> int # alias for numel()
```

将输入Tensor中含有的元素数量输出

****参数:

input (Tensor) – the input tensor.

## 类别

### torch.nn.Module

参数： 
- training (bool)

#### 方法

##### apply(fn)

将fn迭代地应用到所有子模块上，包括自己

返回自己

##### modules()

model.modules()返回一个迭代器，能够迭代遍历模型的所有子层

先从整个Net开始，然后遍历Net下面的子层，再遍历子层的子层……

##### children()

返回直接子模块的迭代器，和modules()方法不同，children()只能迭代子层的子层

##### named_modules()

有名字的modules()方法，该迭代器除了返回模型的所有子层之外，还会返回这些层的名字（如果没有命名就是pytorch按照规则命名的）

如果想要统一修改某些层（比如所有的conv）：

```python
for name, layer in model.named_modules():
  if "conv" in name:
    ...
# 或者
for layer in model.modules():
  if isinstance(layer, nn.Conv2d):
    ...
```

##### named_children()

带名字的children()方法

##### parameters():

返回迭代器，能够迭代module的所有参数

##### named_parameters()

带有名字的parameters()方法

##### eval()

将模块设置为evaluation模式

等同于train(False)

##### state_dict()

返回包含了module所有state的字典

state包括了所有可以训练的layer，dict中key是名字，dict[key]内是参数

例如：

```python
model.state_dict().keys 
# odict_keys(['architecture.bias', 'preprocess.conv1.weight', 'preprocess.bn1.weight', 'preporcess.bn1.bias',...])
type(model.state_dict()['proprocess.bottleneck.1.conv1.weight'])
# torch.Tensor
```

#### 子类

##### torch.nn.Linear

torch的神经网络子模块：线性模块

Parameters:
- in_featues (int)
- out_features (int)
- bias (bool)

输入为(N, \*, Hin), Hin是in_features的值

输出为(N, \*, Hout), Hout是out_features的值


##### torch.nn.Conv2d

Parameters:
- in_channels (int)
- out_channels (int)
- kernel_size (int or tuple)
- stride (int or tuple)
- padding (int or tuple)
- padding_mode (string)
- dilation (int or tuple)
- groups (int): 分组卷积使用的参数 默认是1
- bias (bool)

##### torch.nn.Upsample

可以做最近邻、线性、双线性、双三次、trilinear的上采样

##### torch.nn.MSELoss

继承自_Loss的子类

其实也是module 震撼我妈

### torch.Tensor

#### 子类

##### torch.nn.parameter.Parameter

Tensor的一种，当Parameter是Module的属性的时候，它会自动地被加到Module的参数列表中（会出现在parameter()迭代器中）。

###### 参数
- data(Tensor)
- requires_grad(bool) :默认为True，使用requires_grad_()方法可以进行更改

### torch.optim.Optimizer

所有optimizer的父类

#### 参数

params(iterable): 可迭代对象，torch.Tensor或者dict，指定哪些张量会被优化

#### 方法

##### step()

执行单个优化步骤，一旦使用backward计算出梯度，就可以调用该函数。

##### 参数

closure(callable)：一个重新评估模型并且返回损失的闭包。（

### torch.optim._LRScheduler

用来更新学习率的类

更新学习率需要在optimizer的更新之后应用

