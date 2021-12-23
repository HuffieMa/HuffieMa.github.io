---
title: 百度网盘不限速下载方法
date: 1946-02-14 00:00:00
description: 使用油猴插件+IDM直链下载实现百度网盘不限速下载。
tags:
- <font color="white"> WOW </font>
notshow: true
---


## 一、安装TamperMonkey扩展程序（油猴）
需要使用Edge浏览器或Chrome浏览器。

### 1.1 如何使用Edge浏览器安装油猴
使用Edge浏览器安装油猴十分简单，直接进入[【扩展应用商店】](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepeloendndfphd?hl=zh-CN)安装即可。
### 1.2 如何使用Chrome浏览器安装油猴
1. 如果可以科学上网，进入[【Chrome扩展程序商店】](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=zh-CN)，点击右侧的添加至chrome即可。
ps.查外文文献查资料会经常需要科学上网。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230923512-tampermonkey.png)
2. 如果无法打开上面的网页，可以[【点此下载】](https://huffie.lanzouw.com/i6TuUuhjdyd
)离线包。①将下载的压缩文件解压；②打开浏览器扩展程序管理页面；③右上角打开开发者模式；④将解压出来的【TamperMonkey.crx】文件拖到到此页面。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230924215-chrome-extension.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230924091-chrome-extension.png)

## 二、安装油猴脚本

这一步不论什么浏览器都一样。打开[【此网页】](https://greasyfork.org/zh-CN/scripts/418182-%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98%E7%AE%80%E6%98%93%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B-%E7%9B%B4%E9%93%BE%E4%B8%8B%E8%BD%BD%E5%A4%8D%E6%B4%BB%E7%89%88)，安装脚本即可。

ps. 油猴是一个非常实用的插件，GreasyFork里面有很多实用的脚本，想了解的可以自行探索。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230925109-greasyfork.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230927139-baiduwangpan.png)

## 三、开始下载
### 3.1 准备IDM
如果你已经在使用IDM，那么可以跳过这一步。

如果没有，可以使用刚才解压的文件夹中的IDM绿色版。
1. 将压缩包解压后运行【绿化.bat】；
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230928396-lvhua.png)
2. 运行【IDMan.exe】
3. 打开【选项】菜单，点击【下载】栏，将用户代理UA修改为：**softxm;netdisk**
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230929578-daili.png)
4. 点击【连接】栏，将最大连接数设置为**4**，点击【确定】
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230929559-linknumber.png)

### 3.2 选择文件下载
1. 打开[【百度网盘网页版】](https://pan.baidu.com/)，选择一个要下载的文件。（注意只能是一个文件，不能是文件夹）。

2. 点击上方的简易下载助手下载。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230929410-xiazai1.png)
3. 点击【获取直链地址】，并【复制直链地址】
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230930860-xiazai2.png)
4. 打开IDM，选择新建下载任务，粘贴刚才的直链地址进行下载。
下载速度根据当前网络状况，校园网一般在**2MB/s~10MB/s**
![](https://gitee.com/huffiema/pictures/raw/master/image/202112230930623-ceshi.png)