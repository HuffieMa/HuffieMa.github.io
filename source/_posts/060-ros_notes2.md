---
title: 【ROS学习笔记】（二）工作空间与功能包的创建
date: 2021-02-23 13:55:33
description: 工作空间是存放工程开发相关文件的文件夹，类似windows中使用ide时创建的工程。工作空间包含的文件夹包括……
categories:
- 机器人
- ROS
tags:
- 笔记
- ros
---



### 工作空间的概念
工作空间是存放工程开发相关文件的文件夹，类似windows中使用ide时创建的工程。
### 工作空间包括的文件夹
1. src：代码空间
2. build：编译空间，编译过程中的中间文件，一般用不到
3. devel：开发空间，放置开发过程中的可执行文件、库等
4. install：安装空间

### 创建工作空间

#### 1. 创建工作空间
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
```
#### 2. 编译工作空间
```bash
cd ~/catkin_ws
catkin_make
catkin_make install #产生install文件夹
```
#### 3. 设置环境变量
```bash
source devel/setup.bash
```
#### 4. 检查环境变量
```bash
echo $ROS_PACKAGE_PATH
```
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231647957-ros-notes2-1.png)

### 创建功能包
`catkin_creat_pkg <package_name> [depend1] [depend2] [depend3]`
#### 1. 创建功能包
```bash
cd ~/catkin_ws/src
catkin_create_pkg test_pkg std_msgs rospy roscpp
```
*注：功能包要放在src文件夹下，同一个工作空间不能有同名的功能包*

创建功能包后，在功能包test_pkg文件夹下有**src、include**文件夹和**package.xml、CMakeLists.txt**文件

(1)src文件夹：放置代码文件
(2)include文件夹：放置头文件
(3)package.xml：与功能包相关的信息
（如名字、版本号、许可证、作者信息、功能包的依赖信息等）
(4)CMakeLists.txt：描述功能包的编译规则
#### 2. 编译功能包
```bash
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231647602-ros-notes2-2.png)