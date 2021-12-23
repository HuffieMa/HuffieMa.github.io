---
title: 数字化方法基础（三）_导入本地模型
date: 2019-10-29 20:44:07
description: 全部教程链接：此为其中的第三部分。图形的生成需要消耗一定的时间，简单的模型可能没有什么感觉，但是在模型十分复杂时，模型的生成就需要相当长的时间，这是我们不能忍受的。
categories:
- 机器人
- OpenGL
tags:
- 笔记
- opengl
---

全部教程链接：
[https://blog.csdn.net/weixin_44543463/article/details/102650117#_490](https://blog.csdn.net/weixin_44543463/article/details/102650117#_490)
此为其中的第三部分
#  Chapter 6  导入本地模型

图形的生成需要消耗一定的时间，简单的模型可能没有什么感觉，但是在模型十分复杂时，模型的生成就需要相当长的时间，这是我们不能忍受的。因此，将模型保存为本地文件，使用时直接加载进来，这就变得十分必要了，本节主要讲如何将创建一个列表以及如何加载一个列表。

##  如何创建一个列表

列表的基本原理就是将之前写的**从glPolygonMode、glBegin开始，到glEnd**将这些代码**用一行glCallList(DrawList)代替**，其中DrawList内存放的就是之前生成四面体的代码了。glCallList就相当于把原来的四面体代码加载进来。
那如何将原来的四面体代码创建为一个列表供glCallList读取呢，过程十分简单，只需要按以下步骤即可：
1、在整个文件开头部分**定义一个GLuint类型的全局变量**（因为这个变量要在不同的函数使用，故须定义为全局变量）

```c
GLuint DrawList;
```

2、将RenderScene函数（就是之前写glbegin和glEnd的地方）中的**有关三角形的代码全部用glCallList函数代替**

![image-20211223100655803](C:\Users\82785\AppData\Roaming\Typora\typora-user-images\image-20211223100655803.png)
3、在SetupRC函数中的最后**新建列表**，**框架**如下
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231007333-numerical-recipe-27.png)
4、框架写好之后在图中注释位置**插入画四面体的代码**，插入后结果如下图
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231007814-numerical-28.png)
5、至此一个存有四面体列表就新建好了，点击调试运行即可看到和以前一样的四面体。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231007227-numerical-recipe-29.png)

##  如何读取本地模型

当我们需要读取本地文件中的模型时，如何操作呢
1、既然要读取文件中的模型，首先肯定要打开文件，在创建列表的代码之前插入如下三行代码
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231008514-numerical-recipe-30.png)
（注意，if stream的括号内为文件的路径，其中的\都要写成\\，因为在C语言字符串中，\表示转义，\\\才表示一个\）
（注意，ifstream若要使用需要先在开头插入以下两行引入头文件同时设置环境)

```c
#include<fstream>
using namespace std;
```

2、在定义几个数组用来存放一会要读取的数据
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231008162-numerical-recipe-31.png)
3、然后，将之前画四面体的代码，更改为读取文件的代码，更换后的框架如下，其中in每次读取一串字符（到空格或换行停止)，**in >> String0指的是将读取到的字符存入String0中**

```cpp
	DrawList = glGenLists(1);
	glNewList(DrawList,GL_COMPILE);
	glPolygonMode(GL_BACK,GL_LINE);
	//在↓插入代码
	in >> String0 >> String0;//这就表示将两个字符串先后存入到String0中
	//因为如下图在读取到有用数据之前有两个没用的单词，需要读取两次
	while(strcmp(String0,"end"))//读到的字符串为end则退出循环
	{
		in >> Points[0] >> Points[1] >> Points[2];
//因为刚才已经读掉了前两个没用的字符串，因此直接读取三个坐标到Points里
		in >> String0 >> Points[3] >> Points[4] >> Points[5];
//如下图读完第一组坐标后会遇到 vertex这个单词，需要读到垃圾桶（String0）里再读坐标
		in >> String0 >> Points[6] >> Points[7] >> Points[8];
//同上
		glColor3ub(200,200,2);
		glBegin(GL_TRIANGLES);
		DrawTriangle(Points,Points+3,Points+6);
//这三行时画一个三角形，根据刚才读到的三个点
		in >> String0;
	}
	//在↑插入代码
	glEndList();
```

（因为用到了strcmp函数，需要引入头文件#include<string.h>）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231009244-numerical-recipe-32.png)

![](https://gitee.com/huffiema/pictures/raw/master/image/202112231009411-numerical-recipe-33.png)
注意一下，计算机里的图像**无论是平面还是曲面，都是由无数个三角形组成的**，只不过三角形数量无比多时，我们看起来它就是一个曲面，Part1.TXT文件中也是，每读取到三个点就画一个三角形，许许多多个三角形就会组成一个立体图形。
4、至此，如何从文件中导入立体模型就完成了，点击调试，即可看到一个正方体
6、那么对于给定的STL文件如何读取？首先右击Part2.STL，用记事本打开，看到文件内容如下
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231010481-numerical-recipe-34.png)
这看起来和之前差不多，只是他多给了一个法向量，没用的字符串多了一些而已，你可以不用他给的法向量，只读取三个坐标然后自己计算法向量，也可以读取法向量，这个时候 DrawTriangle函数就不需要计算法向量了，直接四行代码就ok，和之前一样，每一次in >> String0操作就读掉一个没用的字符串，自己编写代码就可实现将STL文件中的所有点全部读取出来
需要注意的是，**每次循环结束**的时候都要保证**String内存放**的是**facet或者最后的endsolid**这个单词，以保证循环可以正常退出

```cpp
void DrawTriangle(float a[3],float b[3],float c[3],float n[3])
{
	//float n[3];
	//project(a,b,c,n);
	glNormal3fv(n);
	glVertex3fv(a);
	glVertex3fv(b);
	glVertex3fv(c);
}
```

PS.如果程序出现错误，如何进行调试呢，首先在while循环里第一句前面设置断点，如下图
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231010555-numerical-recipe-35.png)
然后点击单步执行第二个按钮
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231010062-numerical-recipe-36.png)
每次循环读9个点,查看你读取到的点的值是否与文件中的坐标值一一对应，其中012对应第一行3个点，345对应第二行三个点，678对应第三行。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231011562-numerical-recipe-37.png)

**Continue**