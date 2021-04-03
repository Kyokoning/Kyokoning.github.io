---
layout:     post
title:      "pytorch中hook的使用"
subtitle:   ""
date:       2020-12-12 21:16:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - pytorch
    - 深度学习
---

[TOC]

### 摘要

NAS中使用FLOPs等做constraints是很常见的方法，使用hook计算pytorch module MACs和Params也是很常见的方法。

将两者结合希望能有好用处。

### 参考

[THOP: Pytorch-OpCounter](https://github.com/Lyken17/pytorch-OpCounter)

[Pytorch中autograd以及hook函数详解](https://oldpan.me/archives/pytorch-autograd-hook)

