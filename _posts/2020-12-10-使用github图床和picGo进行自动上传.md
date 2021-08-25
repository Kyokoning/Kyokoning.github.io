---
layout:     post
title:      "使用github图床和picGo自动上传图片"
subtitle:   "要进行笔记迁移 好累"
date:       2020-12-10 15:40:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - markdown
---


[TOC]

### Abstract

---

最近在看论文的时候对我手边的记录环境感到烦躁，——evernote虽然用得久，但经常卡顿，而且图片上传只到私域，很不利于未来的可扩展性。

（主要是贫穷买不起带会员，都怪缪）

因此今天开始尝试把paper reading从evernote迁移到sublime+typora这边，用更科学的方法记录。

主要问题就是图床，本文采用github图床，突出一个省心。考察了七牛图床还需要备案的域名，遂放弃。

环境：osx10.15.6

### 步骤

---


1. 使用PicGo可以自动上传图片

```bash
// 使用node package manager安装picGo-Core
brew install node
// 查看是否安装node成功
node -v
npm -v
// 安装picgo
npm install picgo -g
// 查看是否安装picgo成功
picgo -v
// 进行配置
subl ~/.picgo/config.json
```

[配置文件的document](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A)

```json
{
  "picBed": {
    "uploader": "github", // 默认上传目标
    "github": {
 			 "repo": "", // 仓库名，格式是username/reponame
 			 "token": "", // github token
 			 "path": "", // 自定义存储路径，比如img/
 			 "customUrl": "", // 自定义域名，注意要加http://或者https://
 			 "branch": "", // 分支名，默认是main
		},
  "picgoPlugins": {}
}
```

2. 设置完之后，命令行中使用`picgo u <图像文件>`上传图像，可以检查是否设置正确。

3. 打开typora-preference，在图片选项夹中选择Customer Command：<img src="https://raw.githubusercontent.com/Kyokoning/Kyokoning.github.io/main/img/paper-cut/image-20201210180228213.png" alt="image-20201210180228213" style="zoom:50%;" />

   自定义命令设置为<node位置> <picgo位置> u

   这两个位置通过`which node`和`which picgo`获得。

   点击验证图片上传选项，如果通过即可。

4. 注意，使用github图床如果图像名字一样上传是会失败的。

