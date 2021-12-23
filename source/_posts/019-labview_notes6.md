---
title: LabView学习笔记（六）：while循环与for循环
date: 2021-01-12 15:29:38
description: while循环至少执行一次，for循环可以执行0次，while循环自动输出最后一次执行的值，for循环自动输出一个数组。可以右键单击while循环的边框，在右键菜单中将while循环转换为for循环。
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

## while循环（图片循环播放程序）
实验：完成三张图片的循环放映
1. 插入一个图片下拉列表，并导入n张图片
![image-20211223110219783](C:\Users\82785\AppData\Roaming\Typora\typora-user-images\image-20211223110219783.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231102463-labview-notes6-2.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231102640-labview-notes6-3.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231103974-labview-notes6-4.png)
2. 打开程序框图，利用While循环实现图片的循环播放，首先将图片下拉列表转换为显示控件
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231103789-labview-notes6-5.png)
3. 创建一个While循环
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231103002-labview-notes6-6.png)
4. 因下拉图片列表中各个图片的值为0，1，2……n，利用循环次数与n的余数作为图片的选择依据（n为图片个数），插入数值中的商与余树控件并连线
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231103372-labview-notes6-7.png)
在我的程序中图片数是3所以除数为3
5. 创建停止条件
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231103976-labview-notes6-8.png)
6. 回到前面板中添加一个旋钮，用于调整图片切换速度
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231104493-labview-notes6-9.png)
7. 在while循环中插入一个等待时间，等待时间的输入端以毫秒作为单位，同时考虑旋钮越大图片切换速度应该越快，因此将旋钮的数值取倒数再乘1000作为while循环的等待时间
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231104454-labview-notes6-10.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231104777-labview-notes6-11.png)
8. 运行程序，即可观察到图片循环播放，拖动旋钮可以看到图片切换速度也会随之变化。

## for循环
1. for循环的创建
* 创建for循环的方法和while循环类似
* 可以右键单击while循环的边框，在右键菜单中将while循环转换为for循环
2. for循环的接线端
* N为循环次数，循环次数必须指定为非负整数（如果将双精度浮点数值连接至总线接线端，LabView将把较长的数值转换为32位有符号整数）
* 为了避免强制转换，以增强程序性能，选择匹配的数据类型，或者通过编程进行数据类型的转换
3. 与while循环的区别
* while循环至少执行一次，for循环可以执行0次
* while循环自动输出最后一次执行的值，for循环自动输出一个数组