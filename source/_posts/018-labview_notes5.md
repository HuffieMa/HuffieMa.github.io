---
title: LabView学习笔记（五）：数据类型综合实验
date: 2021-01-11 15:17:35
description: 输出正弦波信号，频率0-50M；采样率10M、50M、100M可选；检测信号频率；输出采样信号的功率谱，如果频率或采样率发生变化，重新开始平均过程
categories:
- 嵌入式
- LabVIEW
tags:
- 笔记
- labview
---

**Labview学习笔记**：
[LabView学习笔记（一）：基础介绍](https://blog.csdn.net/weixin_44543463/article/details/112325523)
[LabView学习笔记（二）：滤波器实验](https://blog.csdn.net/weixin_44543463/article/details/112329185)
[LabView学习笔记（三）：基本控件](https://blog.csdn.net/weixin_44543463/article/details/112364388)
[LabView学习笔记（四）：动态数据类型](https://blog.csdn.net/weixin_44543463/article/details/112366358)
[LabView学习笔记（五）：数据类型综合实验](https://blog.csdn.net/weixin_44543463/article/details/112392799)
[LabView学习笔记（六）：while循环与for循环](https://blog.csdn.net/weixin_44543463/article/details/112393383)
[LabView学习笔记（七）：变量与移位寄存器](https://blog.csdn.net/weixin_44543463/article/details/112431393)
[LabView学习笔记（八）：属性节点](https://blog.csdn.net/weixin_44543463/article/details/112470713)
[LabView学习笔记（九）：数组与簇](https://blog.csdn.net/weixin_44543463/article/details/112529983)
[LabView学习笔记（十）：条件结构](https://blog.csdn.net/weixin_44543463/article/details/112571924)
[其它实验过程记录](https://blog.csdn.net/weixin_44543463/category_10714833.html)

---

## 任务要求
1. 输出正弦波信号，频率0-50M
2. 采样率10M、50M、100M可选
3. 检测信号频率
4. 输出采样信号的功率谱，如果频率或采样率发生变化，重新开始平均过程

## 实现过程
1. 在程序框图中创建基本函数发生器，按下Ctrl+H查看即时帮助中的接口说明
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231056843-labview-notes5-1.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231056869-labview-notes5-2.png)
2. 按照任务要求配置各个接口，首先在信号类型处右键，创建常量（正弦波）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231057916-labview-notes5-3.png)
3. 在频率、采样信息处右键创建输入控件
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231057344-labview-notes5-4.png)
4. 添加两个波形测量的Express VI，分别是提取单频信息、FFT功率谱和PSD
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231057877-labview-notes5-5.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231057962-labview-notes5-6.png)
5. 在 提取单频信息 的Express VI的**检测到的功率**的接口，FFT功率谱和PSD 的Express VI**功率谱/PSD**接口创建显示控件
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231058600-labview-notes5-7.png)
6. 在FFT功率谱和PSD的Express VI的**显示为DB**接口创建常量并设置为**True**
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231058453-labview-notes5-8.png)
7. 在FFT功率谱和PSD的Express VI的**平均参数**接口创建常量并设置为**RMS均方根平均方式**
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231058660-labview-notes5-9.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231058145-labview-notes5-10.png)
8. 因需要重新开始平均所以在**重新开始平均**接口处创建常量并选择为**真**
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231059510-labview-notes5-11.png)
9. 切换回前面板，将功率谱的显示方式替换为波形图，并将频率的显示方式替换为旋钮
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231059800-labview-notes5-12.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231059373-labview-notes5-13.png)
10. 修改旋钮周围的刻度
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231059667-labview-notes5-14.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231100465-labview-notes5-15.png)
11. 将采样信息替换为文本下拉列表，然后右键-编辑项，修改下拉列表的菜单，并设置默认值为50M
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231100878-labview-notes5-16.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231100461-labview-notes5-17.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231101223-labview-notes5-18.png)
12. 修改检测到的频率的显示格式
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231101135-labview-notes5-19.png)
13. 进行简单外观修饰后运行程序
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231101949-labview-notes5-20.png)