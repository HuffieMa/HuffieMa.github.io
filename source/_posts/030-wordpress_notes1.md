---
title: WordPress学习笔记（一）文章操作
date: 2021-01-22 17:07:13
description: 对于一个网站来说，内容是最重要的一部分，用户之所以访问你的网站，也是因为你的内容。在WordPress中，内容主要分成两个部分：文章和页面。文章：用于发布网站的主要内容（如博客类网站，文章处发布博文）页面：用于发布网站的其他内容（如博客类网站，页面处发布博主/网站信息）。
categories:
- 程序设计
- 网站
tags:
- 笔记
- wordpress
---

## 一、简述

### 1. 网站的内容
对于一个网站来说，内容是最重要的一部分，用户之所以访问你的网站，也是因为你的内容。在WordPress中，内容主要分成两个部分：文章和页面。
- 文章：用于发布网站的主要内容（如博客类网站，文章处发布博文）
- 页面：用于发布网站的其他内容（如博客类网站，页面处发布博主/网站信息）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231122275-wordpress-notes1-1.png)
### 2. 网站的规划
（1）划分出网站的主要内容和其他内容
（2）对主要内容进行分门别类，划分出分类目录
（3）不需要事先划分标签

>**分类目录**：对文章按内容进行分类
>**标签**：可以理解为是一种标记，通过给文章添加一个标记，如果需要查看带有某个标记的文章的时候，wordpress就能快速筛选出来。

![](https://gitee.com/huffiema/pictures/raw/master/image/202112231123221-wordpress-notes1-2.png)

## 二、文章
- 右边可以看到文章的发布信息、状态、分类目录、标签、特色图片等信息
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231123743-wordpress-notes1-3.png)
- 点击右上角显示选项可以看到更多信息，这里可以先把所有复选框都选上，后面一个一个看他们的作用。（我们的选项可能不一样，这是因为安装的插件不同导致的，这个不用在意）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231123157-wordpress-notes1-4.png)
1. **标题**：从上到下，第一个就是文章内容的标题，这里就不多说。
2. **添加媒体**：可以上传图片等文件，插入进文章中光标所在位置
3. **文章摘要**：在文章内容下面，可以看到文章摘要的填写框，文章摘要就是文章主要内容的概述，作用为在网站的文章列表中显示摘要，让用户快速的了解文章的主要内容，如果用户感兴趣的话可以进一步查看内容。
4. **发送Trackback**：如果应用或借鉴了其他人的文章，可以在此处填写ulr通知对方，这个功能目前很少使用。
5. **自定义栏目**：在正文内无法添加，需要添加更多的内容，可以在自定义栏目中实现。
6. **讨论**：允许评论勾选则允许评论，不勾选则不允许用户评论
7. **评论**：可以添加，或者管理评论
8. **别名**：修改链接网址，使网址更符合搜索引擎的索引要求
9. **标签**：可以给文章打上标记，将来如果想查看文章，只需要使用标签即可。
10. **特色图像**：相当于文章的缩略图