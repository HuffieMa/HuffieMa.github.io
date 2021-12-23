---
title: 【C++笔记】运算符重载
date: 2021-03-09 08:25:50
description: 运算符重载的目的是对已有的运算符重新定义，赋予其另一种功能，以适应不同的数据类型。包括加号、左移、递增、赋值、关系、函数调用等运算符重载。
categories:
- 程序设计
- C++
tags:
- 笔记
- c++
---

运算符重载的目的是对已有的运算符重新定义，赋予其另一种功能，以适应不同的数据类型。

### 一、加号运算符重载

作用：实现两个自定义数据类型的加法运算

**1.1 通过成员函数重载+号**

```c++
例：
class Person{
    Person operator+(Person &p){
		Person temp;
		temp.m_A = this->m_A + p.m_A;
		temp.m_B = this->m_B + p.m_B;
		return temp;
	}
    int m_A;
    int m_B;
};
```

调用方法：

1. 本质调用：`Person p3 = p1.operator+(p2);`
2. 简化调用：`Person p3 = p1 + p2;`

**1.2 通过全局函数重载+号**

```c++
Person operator+(Person &p1, Person &p2){
	Person temp;
	temp.m_A = p1.m_A + p2.m_A;
	temp.m_B = p1.m_B + p2.m_B;
	return temp;
}
Person operator+(Person &p1, int num){
	Person temp;
	temp.m_A = p1.m_A + num;
	temp.m_B = p1.m_B + num;
	return temp;
}
```

调用方法：

1. 本质调用：`Person p3 = operator+(p1, p2);`
2. 简化调用：`Person p3 = p1 + p2;`

运算符重载也可以发生函数重载：

```c++
Person p3 = p1 + p2;
Person p4 = p1 + 100;
```

**1.3 注意事项**：

* 对于内置的数据类型的表达式的运算符是不可能改变的
* 不要滥用运算符重载

### 二、左移运算符重载

**通过全局函数重载<<左移运算符**

```c++
ostream& operator<<(ostream &cout,Person &p){
	cout << "p.m_A = " << p.m_A << endl;
	cout << "p.m_B = " << p.m_B << endl;
	return cout;
}
```

* 选中cout，右键转到声明，可以看到cout属于ostream这个类
* 返回cout是为了实现链式编程，使得可以无限追加<<
* 不通过成员函数重载是因为，成员函数重载只能实现p.operator<<(cout)，即p<<cout，与预期不符。

调用方法：

`cout << p << endl;`

### 三、递增运算符重载

```c++
class MyInteger{
public:
	MyInteger(){
		m_Num = 0;
	}
	//重载前置++运算符
	MyInteger& operator++(){
		++m_Num;
		return *this;
	}
	//重载后置++运算符	此处的int代表占位参数，可以用于区分前置和后置递增
	MyInteger operator++(int){
		MyInteger temp = *this;
		m_Num++;
		return temp;
	}

private:
	int m_Num;
};
```

前置++：

* 返回值是引用，是因为需要实现++(++a)，保证自增的都是同一个数据

后置++：

* 因为后置++要先返回当前值，再递增。因此先把当前值记录下来，递增之后，再返回记录值。
* 返回值以值传递形式，是因为返回的是局部对象temp，局部对象不能通过引用返回。

### 四、赋值运算符重载

c++编译器至少给一个类添加四个函数

1. 默认构造函数（无参，函数体为空）
2. 默认析构函数（无参，函数体为空）
3. 默认拷贝构造函数，对属性进行值拷贝
4. 赋值运算符 operator=对属性进行值拷贝

如果类中有属性指向堆区，做赋值操作时也会出现深浅拷贝问题。

解决方法：利用深拷贝，解决浅拷贝带来的问题

```c++
#include<iostream>
using namespace std;

class Person{
public:
	Person(int age){
		m_Age = new int(age);
	}

	~Person(){
		if(m_Age != NULL){
			delete m_Age;
			m_Age = NULL;
		}
	}

	//重载赋值运算符
	Person& operator=(Person &p){
		//先判断是否有属性在堆区，如果有，先释放干净，再深拷贝
		if(m_Age != NULL){
			delete m_Age;
			m_Age = NULL;
		}
		//进行深拷贝
		m_Age = new int(*p.m_Age);
		return *this;
	}

	int *m_Age;
};

void test01(){
	Person p1(18);
	Person p2(20);
	Person p3(24);
	p3 = p2 = p1;

	cout << "p1.m_Age = " << *p1.m_Age << endl;
	cout << "p2.m_Age = " << *p2.m_Age << endl;
	cout << "p3.m_Age = " << *p3.m_Age << endl;
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

注意事项：

* 重载=的逻辑是，如p2=p1，先释放p2内的属性（因为浅拷贝p2和p1内的m_Age指向同一块内存），然后再重新开辟内存空间进行深拷贝。
* 返回值是Person&，是为了连续赋值操作

### 五、关系运算符重载

**作用：**重载关系运算符时，可以让两个自定义类型对象进行对比操作。（如==、!=）

```c++
//例：重载==运算符
bool operator==(Person &p){
    if(this->m_Name == p.m_Name && this->m_Age == p.m_Age){
        return true;
    }
    else{
        return false;
    }
}
```

### 六、函数调用运算符重载

* 函数调用运算符是()
* 由于重载后使用方式非常像函数的调用，因此称为仿函数
* 仿函数没有固定写法，非常灵活

```c++
//例：重载()实现自定义打印
class MyPrint{
public:
	void operator()(string test){
		cout << test << endl;
	}
};
---------
//调用方法
	MyPrint myprint;
	myprint("hello world");
```

> 重载()很像函数调用，比如上面的功能也可以用函数实现
>
> ```c++
> void myPrint(string test){
> 	cout << test << endl;
> }
> ---------
> myPrint("hello world")
> ```


  > **参考**：黑马程序员匠心之作|C++教程从0到1入门编程,学习编程不再难
  > **链接**：[https://www.bilibili.com/video/BV1et411b73Z](https://www.bilibili.com/video/BV1et411b73Z)