---
title: WordPress学习笔记（三）其他功能
date: 2021-01-24 14:32:36
description: 媒体库是主要用来管理，你使用wordpress上传的附件的，比如图片、视频等其他文件。 点击左上角可以切换视图（列表/缩略图）。在评论内容处可以管理评论，更换不同的主题，网站的视觉效果会发生改变。用户看到的网站内容也会发生改变。站点的功能也会发生变化。
categories:
- 程序设计
- 网站
tags:
- 笔记
- wordpress
---

## 一、媒体库

媒体库是主要用来管理，你使用wordpress上传的附件的，比如图片、视频等其他文件。 点击左上角可以切换视图（列表/缩略图）
 ### 媒体文件的管理
1. 编辑：可以修改图片的的标题，说明文字，替代文本。替代文本是当图片没有办法正常显示的时候，会用文本代替图片。
2. 永久删除：在媒体库中删除媒体，已经在文章中添加过的不受影响
3. 查看：以网页的形式查看图片
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231124625-wordpress-notes3-1.png)
 ### 媒体文件添加
 1. 在此处可以上传到上传文件最大允许尺寸为2M
 2. 常用的图片格式、文档格式、压缩格式都可以上传。可以利用这里上传文件供用户下载。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231124661-wordpress-notes3-2.png)

## 二、评论管理
1. 列表从左到右依次是：评论的用户，评论内容，用户评论的文章，评论时间。
2. 在评论内容处可以管理评论，具体操作有
（1）驳回/批准：wordpress默认设置用户发表评论，批准后才会在网页显示
（2）回复：就是回复用户的评论
（3）编辑：可以修改用户的评论
（4）垃圾评论和移至回收站操作后，评论都不会在网页中显示。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231125996-wordpress-notes3-3.png)

## 三、用户管理
### 添加用户
可以在此给网站添加用户，一般是不会手动添加用户的，手动添加用户一般只用来添加管理员，普通用户通常是会有注册渠道。
填写用户名，电子邮件，名字，姓氏，密码，选择用户角色后即可完成用户的添加。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231125420-wordpress-notes3-4.png)

### 用户资料
点击个人资料即可看到自己的资料
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231125017-wordpress-notes3-5.png)

1. 可视化编辑器
不使用可视化编辑器：
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231125549-wordpress-notes3-6.png)
使用可视化编辑器
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231126322-wordpress-notes3-7.png)
2. 管理界面的配色：后台左侧和上侧的颜色
3. 工具栏：在登录之后，打开自己的网站，会看到最上面有一条工具条。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231126870-wordpress-notes3-8.png)
4. 资料图片：需要到gravatar网站上注册账户，并设置头像。当在wordpress的网站中使用相同的邮件账户注册会员，那么wordpress就会根据邮件账户信息，从gravatar网站中获取头像
### 管理用户
在所有用户页面内可以管理此网站的所有用户
在这里插入图片描述
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231126221-wordpress-notes3-9.png)

## 四、工具

### 快速发布
将按钮拖动到收藏夹栏即可添加这个工具。再打开别人的网站时，点击快速发布按钮，可以将该网页的标题，内容，图片等copy下来形成一个文章。
### 直接链接
类似快速发布，点击直接连接按钮，可以看到最上方有一栏可以输入url，找到想要剪辑的网页，将url复制到此栏即可生成一篇文章。
### 导入和导出
导入可以从其它博客平台等网站，将自己的文章和评论等导入到此网站。到处则是创建一个xml文件，保存网站的内容。

## 五、外观
### 主题
1. 主题的作用
更换不同的主题，网站的视觉效果会发生改变。用户看到的网站内容也会发生改变。站点的功能也会发生变化。
2. 主题的安装方法
点击添加主题即可进入安装页面，可以在此页面安装主题
（1）在线安装：在wordpress的特色、热门、最新等栏目中选择主题，也可以搜索主题安装。安装后点击实时预览可以看到网站更换主题的效果。点击启用即可更换主题。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231126493-wordpress-notes3-10.png)
（2）手动安装：将主题下载到本地，点击上传主题，选择下载好的主题zip文件，点击现在安装即可。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231127787-wordpress-notes3-11.png)
（3)直接安装：直接将解压后的主题文件夹，放置在wp-content/themes/文件夹内。回到主提页面，刷新一下即可看到刚才安装的主题。
3. 自定义主题
点击自定义按钮后，可以看到左侧是自定义的栏目（不同的主题栏目会不一样），右侧是实时效果预览
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231127605-wordpress-notes3-12.png)
### 小工具
有的主题没有提供这个功能，有没有这个功能是由主题决定的。
1. 小工具右侧可以看到一些容器，修改这些容器可以更改网页的效果。
2. 小工具左侧可用的选项，可以拖动到右面的容器中使用。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231127711-wordpress-notes3-13.png)
## 六、设置
### 常规设置
1. 站点标题：网站的名称
2. 副标题：一般情况下，显示在网站的标题旁边 
3. wordpress地址和站点地址一般使用默认
4. 电子邮件地址：用于接收站点相关通知的邮
5. 成员资格：网站是否允许其他人注册
6. 新用户默认角色：考虑权限以及安全问题，订阅者权限即可。
7. ICP备案号：可以填写网站的备案号，是否会在网站显示取决于主题。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231127549-wordpress-notes3-14.png)
### 撰写设置
1. 默认文章分类：发布文章时没有勾选分类目录时，wordpress会自动将这篇文章放到此处设置的分类目录里面
2. 更新服务：在更新服务里面填写的网址，当发布新的内容的时候，wordpress会自动通知此处的链接地址。（主要用于搜索优化）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231128293-wordpress-notes3-15.png)
### 阅读设置
1. 首页显示：默认显示最新文章，选择静态页面时可以设置站点首页为后台发布的某张页面
2. Feed中显示最近：用户订阅我们网站内容时，每页显示多少内容
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231128640-wordpress-notes3-16.png)
### 讨论设置
尝试通知文章链接的博客：在发布文章时，如果文章内容发布链接时，如果勾选此选项，则会通知对方我们的链接指向了他们（一般不使用）。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231128717-wordpress-notes3-17.png)

### 多媒体设置
上传图片后，wordpress会自动在此图片基础上转换出不同像素大小的图片。
### 固定链接
通过切换不同的链接结构，可以改变网页网址。更改的主要原因是为了搜索引擎检索的优化。一般使用文章名较好。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231128743-wordpress-notes3-18.png)
自定义结构

| 代码       | 作用       |
| ---------- | ---------- |
| %post_id%  | 内容的编号 |
| %postname% | 内容的名称 |
| %year%     | 发布的年份 |
| %monthnum% | 发布的月份 |
| %day%      | 具体哪一天 |