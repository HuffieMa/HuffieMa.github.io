---
title: RobotStudio创建目标点时出现未找到有效配置的问题
date: 2021-02-07 22:40:27
description: RobotStudio在使用路径和目标点的创建目标点时，有时会出现无法跳转到目标点的问题，错误为未找到有效配置。解决方法1：在基本-设置选择正确的工具坐标，例如夹具的工具坐标。
categories:
- 机器人
- RobotStudio
tags:
- bug解决
- robotstudio
---

#### 问题描述：
RobotStudio在使用路径和目标点的创建目标点时，有时会出现**无法跳转到目标点**的问题，错误为**未找到有效配置**。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231544276-robotstudio-noconfig-1.png)

#### 原因分析：
1. **未使用正确的工具坐标**
2. 目标点的坐标与工具坐标无法对应，**机器人不能实现运动**到指定位置使两坐标系重合。
#### 解决方法：
1. 解决方法1：在基本-设置选择正确的工具坐标，例如夹具的工具坐标。
2. 解决方法2：右键目标点-修改目标-旋转，将坐标系旋转至**工具运动到此位置时的工具坐标系重合**。如果仍然有问题可以多试几个方向，一般不止一个方向可以实现跳转到目标点。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231545842-robotstudio-noconfig-2.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231546698-robotstudio-noconfig-3.png)