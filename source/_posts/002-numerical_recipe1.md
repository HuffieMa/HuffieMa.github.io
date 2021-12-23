---
title: 数字化方法基础（一）_基础操作与生成四面体
date: 2019-10-29 20:39:44
description: 全部教程链接：此为其中的第一部分。Chapter1 VisualStudio2010 Express如何创建新工程。新建一个win32 Console Application工程，选择建立一个空项目（带预编译头的也可以，只不过大多数人不太习惯）。
categories:
- 机器人
- OpenGL
tags:
- 笔记
- opengl
---

全部教程链接：
[https://blog.csdn.net/weixin_44543463/article/details/102650117#_490](https://blog.csdn.net/weixin_44543463/article/details/102650117#_490)
此为其中的第一部分

# Chapter1  VisualStudio2010 Express如何创建新工程

   1、新建一个win32 Console Application工程，选择建立一个空项目（带预编译头的也可以，只不过大多数人不太习惯）

![image-20211223095734449](C:\Users\82785\AppData\Roaming\Typora\typora-user-images\image-20211223095734449.png)

![](https://gitee.com/huffiema/pictures/raw/master/image/202112230957699-numerical-recipe-2.png)
   2、在左侧解决方案资源管理器中右击Source-add-New item，创建一个C++文件

![](https://gitee.com/huffiema/pictures/raw/master/image/202112230958908-numerical-recipe-3.png)
   3、这样就用VS2010创建好了一个简单的工程！

#  Chapter2 SB-WinSRC的使用方法

1、解压压缩包，得到一个SB-WinSRC文件夹
2、打开SB-WinSrc\examples\projects\microsoft\chapt05\shinyjet文件夹中的shinyjet.vcproj文件，如出现以下对话框则一直Next到最后
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112230958911-numerical-recipe-4.png)
3、打开shinyjet.cpp并进行编译（Build solution生成解决方案）
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112230958652-numerical-recipe-5.png)
4、出现图示错误
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112230959276-numerical-recipe-6.png)
5、打开目录\SB-WinSrc\examples\src\shared，找到freeglut_static.lib文件，将它复制到之前打开的shinyjet文件夹内
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112230959001-numerical-recipe-7.png)
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112231000243-numerical-recipe-8.png)
6、再次进行编译（Build solution生成解决方案），出现下图错误
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112231000076-numerical-recipe-9.png)
7、在左侧Solution Explorer（解决方案资源管理器）中右击shinyjet打开属性，将Linker-Input-忽略特定默认库一栏中输入LIBC.lib
 ![](https://gitee.com/huffiema/pictures/raw/master/image/202112231000584-numerical-recipe-10.png)
8、再次编译，成功！

#  Chapter3  用OpenGL生成四面体

## 已知3点求法向量

1、具体思路为先根据已知3点做差求出两个向量，利用两个向量叉乘运算求出法向量，实现过程中尽量避免将所有代码集中到一个函数中，因为后续的操作（如投影点的计算）还需用到求法向量的函数，到时可直接调用。
2、已知2点求向量的函数十分简单，代码如下

```c
void getvector(float a[3],float b[3],float vec[3])
{
	for(int i = 0;i < 3;i++)
		vec[i] = a[i] - b[i];
}
```

3、调用两次上述函数即可获得两个向量，接下来要做的就是拿这两个向量进行叉乘，以得到法向量

```c
//函数中的法向量n[3]是提前在函数外定义的，通过调用函数给n[3]赋值
void crossproject(float vec1[3],float vec2[3],float n[3])
{
	n[0] = vec1[1]*vec2[2]-vec1[2]*vec2[1];
	n[1] = vec1[2]*vec2[0]-vec1[0]*vec2[2];
	n[2] = vec1[0]*vec2[1]-vec1[1]*vec2[0];
}
```

4、将上面两个函数简单封装一下如下

```c
//函数中的法向量n[3]是提前在函数外定义的，通过调用函数给n[3]赋值
void project(float point1[3],float b[3],float c[3],float n[3])
{
	float vec1[3],vec2[3];
	getvector(a,b,vec1);
	getvector(b,c,vec2);
	crossproject(vec1,vec2,n);
}
```

5、这样一个求法向量的函数就写好了，使用方法如下例

```c
	double a[3] = {1.0,0.0,0.0};
	double b[3] = {0.0,1.0,0.0};
	double c[3] = {0.0,0.0,0.0};
	double n[3];
	project(a,b,c,n);
	//调用过project()函数之后，n[3]数组内的值即为法向量
```

##  生成四面体

1、使用OpenGL生成四面体的基本方法为，**给定三个点和一个法向量**，调用OpenDL的库函数，即可**生成一个由这三点围成的三角形平面**，**四个三角形平面即可组成一个四面体**。
2、将课上的shinyjet.cpp模板复制到src相应的文件夹中（\SB-WinSrc\examples\src\chapt05\shinyjet），然后回到project对应文件夹中，打开shinyjet.vcxproj工程，点击调试，成功后出来的应该为一个蓝绿色底的对话框。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231001853-numerical-recipe-11.png)

![](https://gitee.com/huffiema/pictures/raw/master/image/202112231001700-numerical-recipe-12.png)

3、在RenderSenen()函数中的下图位置 **写入glBegin()与glEnd()函数，并在二者之间插入画三角形的代码**。

![](https://gitee.com/huffiema/pictures/raw/master/image/202112231002123-numerical-recipe-13.png)

```c
	float rgfPoints4[12] = {-0.6f,-0.6f,-0.6f,
							0.0f,1.0f,0.0f,
							1.0f,0.0f,0.0f,
							0.0f,0.0f,1.0f};
	//这是定义了一个长为12的数组，每3个元素代表一个点坐标，共4个点
	glColor3ub(255,255,0);
	//设置要生成图形的颜色
	glBegin(GL_TRIANGLES);
	//开始生成三角形
	DrawTriangle(rgfPoints4,rgfPoints4+3,rgfPoints4+6);
	DrawTriangle(rgfPoints4,rgfPoints4+9,rgfPoints4+3);
	DrawTriangle(rgfPoints4+3,rgfPoints4+9,rgfPoints4+6);
	DrawTriangle(rgfPoints4,rgfPoints4+6,rgfPoints4+9);
	//↑函数功能：给定3个点生成一个三角形，调用4次生成4个三角形组成四面体
    glEnd();
    //结束
```

4、在这里，glColor3ub、glBegin，glEnd均是OpenGL的库函数，不需要我们定义，直接调用即可，**需要我们写的是DrawTriangle函数**，接下来我们就开始定义DrawTriangle()，前面已经提到，需要用**3个点和一个法向量**来确定一个平面，因此我们把第一节中生成法向量的函数复制到此文件的开头处，以便调用。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231002324-numerical-recipe-14.png)
5、画三角形的函数如下：

```c
void DrawTriangle(float a[3],float b[3],float c[3])
{
	float n[3];	//定义一个数组用来存放法向量
	project(a,b,c,n);	//调用生成法向量的函数由a,b,c三点生成法向量n
	glNormal3fv(n);
	glVertex3fv(a);
	glVertex3fv(b);
	glVertex3fv(c);		//此四行为利用用库函数，由法向量n和三个点abc生成一个平面
}
```

5、完成上述步骤后，进行调试，即可得到一个四面体
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231003764-numerical-recipe-15.png)