---
title: 【C++笔记】构造函数与析构函数相关知识
date: 2021-03-06 10:46:28
description: 每个对象需要有初始设置以及对象销毁前的清理数据的设置。对象的初始化和清理是两个非常重要的安全问题。一个对象或变量没有初始状态，对其使用后果未知；使用完一个对象或变量，没有及时清理，也会造成一定的安全问题。
categories:
- 程序设计
- C++
tags:
- 笔记
- c++
---

每个对象需要有初始设置以及对象销毁前的清理数据的设置。
### 一、构造函数和析构函数

对象的**初始化和清理**是两个非常重要的安全问题。

* 一个对象或变量没有初始状态，对其使用后果未知
* 使用完一个对象或变量，没有及时清理，也会造成一定的安全问题

C++使用**构造函数和析构函数**解决这两个问题，这**两个函数会被编译器自动调用**，完成对象初始化和清理工作。

对象的初始化和清理工作是编译器强制要我们做的事情，因此**如果我们不提供构造和析构，编译器会提供，编译器提供的构造函数和析构函数是空实现**。

* 构造函数：创建对象时为对象的成员属性赋值
* 析构函数：对象销毁前执行清理工作

**构造函数语法：**`类名(){}`

1. 构造函数，没有返回值也不写void
2. 函数名称与类名相同
3. 构造函数可以有参数，因此可以发生重载
4. 程序在调用对象时会自动调用构造，无须手动调用，而且只会调用一次。

**析构函数语法：**`~类名(){}`

1. 析构函数，没有返回值也不写void
2. 函数名称与类名相同，在名称前加上~
3. 析构函数不可以有参数，因此不可以发生重载
4. 程序在对象销毁前会自动调用析构，无须手动调用，而且只会调用一次

```c++
#include <iostream>
using namespace std;

class Person{
public:
	//构造函数，进行初始化操作
	//构造函数没有返回值 不用写void
	//函数名与类名相同
	//构造函数可以有参数，可以发生重载
	//创建对象的时候，构造函数会自动调用，而且只调用一次
	Person(){
		cout << "Person的构造函数" << endl;
	}

	//析构函数，执行清理操作
	//没有返回值，不写void
	//函数名和类名相同，前面加~
	//不可以有参数，不可以发生重载
	//创建对象的时候，构造函数会自动调用，而且只调用一次
	~Person(){
		cout << "Person的析构函数" << endl;
	}

};

void test(){
	Person p;
}

int main(){
	
	test();
	Person p;

	system("Pause");
	return 0;
}
```

### 二、构造函数的分类及调用

分类方式：

* 按参数分：有参构造和无参构造
* 按类型分：普通构造和拷贝构造

```c++
//普通构造、无参构造（默认构造）
Person(){
	cout << "无参构造函数的调用" << endl;
}
//普通构造、有参构造
Person(int a){
	age = a;
	cout << "有参构造函数的调用" << endl;
}
//拷贝构造
Person(const Person &p){
	//将传入的类中所有的属性传到此对象上
	age = p.age;
	cout << "拷贝构造函数的调用" << endl;
}
```

调用方式：

* 括号法

```c++
Person p1;		//调用无参构造函数
Person p2(10);	//调用有参构造函数
Person p3(p2);	//调用拷贝构造函数
```

> 注：调用默认构造函数的时候，不要加()
>
> 因为 `Person p1();` ，编译器会认为是一个函数的声明

* 显示法

```c++
Person p1;				//调用无参构造函数
Person p2 = Person(10);	//调用有参构造函数
Person p3 = Person(p2);	//调用拷贝构造函数
```

> `Person(10)` 是匿名对象。
>
> 特点：当前行执行结束后，系统会立即回收掉匿名对象。

> 不要用拷贝构造函数初始化匿名对象
>
> `Person(p3);	//报错重定义`
>
> 编译器会认为 Person (p3) 等价于 Person p3;

* 隐式转换法

```c++
Person p1;		//调用无参构造函数
Person p2 = 10;	//调用有参构造函数
Person p3 = p2;	//调用拷贝构造函数
```

> `Person p2 = 10;` 相当于 `Person p2 = Person(10);`

### 三、拷贝构造函数调用时机

C++中拷贝构造函数的调用时机通常有以下情况

* 使用一个已经创建完毕的对象来初始化一个新对象
* 以值传递的方式给函数参数传值

```c++
例：
#include<iostream>
using namespace std;

class Person{
public:
	Person(){
		cout << "默认构造函数调用" << endl;
	}

	Person(int age){
		m_Age = age;
		cout << "有参构造函数调用" << endl;
	}
	
	Person(const Person &p){
		m_Age = p.m_Age;
		cout << "拷贝构造函数调用" << endl;
	}

	~Person(){
		cout << "析构函数调用" << endl;
	}

	int m_Age;

};

//用已经创建完毕的对象初始化一个新对象
void test01(){
	Person p1(20);
	Person p2(p1);	//调用拷贝构造函数

	cout << "p2的年龄为：" << p2.m_Age << endl;
}

//值传递的方式给函数参数传值
void doWork(Person p){}//值传递相当于 Person p = p 的隐式写法
void test02(){
	Person p;
	doWork(p);	//调用拷贝构造函数
}

int main(){

	//test01();
	//test02();
	test03;
	system("pause");
	return 0;
}
```

### 四、构造函数调用规则

默认情况下，c++中类至少有三个函数

* 默认构造函数（无参，函数体为空）
* 默认析构函数（无参，函数体为空）
* 默认拷贝构造函数，对属性值进行拷贝

构造函数调用规则：

* 如果用户定义了有参构造函数，c++不再提供默认无参构造，但是会提供默认拷贝构造
* 如果用户定义拷贝构造函数，c++不会再提供其他构造函数

### 五、深拷贝与浅拷贝

浅拷贝：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作

```c++
例1：浅拷贝的问题，此程序的问题是，m_Height指向的区域，经过两次析构函数的调用，被重复释放了。
#include<iostream>
using namespace std;

class Person{
public:
	Person(){
		cout << "默认构造函数调用" << endl;
	}

	Person(int age, int height){
		m_Age = age;
		m_Height = new int(height);
		cout << "有参构造函数调用" << endl;
	}

	~Person(){
		//析构函数，将堆区开辟的数据做释放操作
		if (m_Height != NULL){
			delete m_Height;
			m_Height = NULL;
		}
		cout << "析构函数调用" << endl;
	}

	int m_Age;
	int *m_Height;	//身高数据开辟到堆区

};


void test01(){
	Person p1(21, 160);

	cout << "P1的年龄为：" << p1.m_Age << "\t身高为：" << *p1.m_Height << endl;

	Person p2(p1);

	cout << "P1的年龄为：" << p1.m_Age << "\t身高为：" << *p2.m_Height << endl;
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

```c++
解决方法：自己实现拷贝构造函数，解决浅拷贝带来的问题
	Person(const Person &p){
		m_Age = p.m_Age;
		//m_Height = p.m_Height;//编译器默认实现的是这行代码
		m_Height = new int(*p.m_Height);
		cout << "拷贝构造函数调用" << endl;
	}

```

### 六、初始化列表

**作用：**为类中的属性进行初始化操作

**语法：**`构造函数(): 属性1(值1),属性2(值2)...{}`

**优点：**类成员存在常量时，只能初始化而不能赋值；类成员存在引用时，只能初始化不能赋值；提高效率。

```c++
#include <iostream>
using namespace std;

class Person{
public:
	//传统的初始化
	//Person(int a, int b, int c){
	//	m_A = a;
	//	m_B = b;
	//	m_C = c;
	//}

	//初始化列表进行初始化
	Person(int a, int b, int c):m_A(a),m_B(b),m_C(c){}
	int m_A;
	int m_B;
	int m_C;
};

void test01(){
	Person p(10,20,30);
	cout << "m_A = " << p.m_A << endl;
	cout << "m_B = " << p.m_B << endl;
	cout << "m_B = " << p.m_B << endl;
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

### 七、类对象作为类成员

C++中类的成员可以是另一个类的对象，**一般称该成员为对象成员**

```c++
class A{};
class B{
    A a;
};
```

当其它类的对象作为本类成员

构造时：先构造类对象，再构造自身。

析构时：顺序与构造相反。

```c++
#include <iostream>
#include <string>
using namespace std;

//手机类
class Phone{
public:
	Phone(string brand){
		m_Brand = brand;
		cout << "Phone的构造函数调用" << endl;
	}

	~Phone(){
		cout << "Phone的析构函数调用" << endl;
	}

	string m_Brand;//品牌
};

//人类
class Person{
public:
	//这里的m_Phone(brand)相当于使用括号法Phone m_Phone(brand)创建对象
	Person(string name, string brand):m_Name(name),m_Phone(brand){
		cout << "Person的构造函数调用" << endl;
	}

	~Person(){
		cout << "Person的析构函数调用" << endl;
	}

	string m_Name;
	Phone m_Phone;
};

void test01(){
	Person p("Huffie","Huawei");

	cout << p.m_Name << " with " << p.m_Phone.m_Brand << endl;
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

### 八、静态成员
静态成员就是在成员变量和成员函数前加上static

* 静态成员变量：
  * 所有对象共享同一份数据
  * 在编译阶段分配内存（全局区）
  * 类内声明，类外初始化

> 静态成员变量有两种访问方式（若为私有权限，类外无法访问）：
>
> 1. 通过对象访问
>
>    ```c++
>    Person p;
>    cout << p.m_A << endl;
>    ```
>
> 2. 通过类名访问
>
>    ```c++
>    cout << Person::m_A << endl;
>    ```

```c++
#include<iostream>
using namespace std;

class Person{
public:
	//类内声明
	static int m_A;
private:
	static int m_B;
};
//类外初始化
int Person::m_A = 100;
int Person::m_B = 200;

void test01(){
	Person p1;
	cout << p1.m_A << endl;	//输出100
	
	Person p2;
	p2.m_A = 200;
	cout << p1.m_A << endl;	//输出200，说明数据共享
}

void test02(){
	//静态成员变量不属于某个对象，所有对象都共享同一份数据，因此静态成员变量有两种访问方式
	//通过对象访问
	Person p;
	cout << p.m_A << endl;
	//通过类名访问
	cout << Person::m_A << endl;
	//cout << Person::m_B << endl;错误，私有权限类外访问不到
}

int main(){

	test01();
	test02();

	system("pause");
	return 0;
}
```

* 静态成员函数
  * 所有对象共享同一个函数
  * 静态成员函数只能访问静态成员变量

> 静态成员函数有两种访问方式（若为私有权限，类外同样无法访问）：
>
> 1. 通过对象访问
>
>    ```c++
>    Person p;
>    p.func();
>    ```
>
> 2. 通过类名访问
>
>    ```c++
>    Person::func();
>    ```

```c++
#include<iostream>
using namespace std;

class Person{
public:
	//静态成员函数
	static void func(){
		m_A = 100;
		//m_B = 200;静态成员函数不可以访问非静态成员变量
		cout << "static void func的调用" << endl;
	}

	//静态成员变量
	static int m_A;
	//非静态成员变量
	int m_B;

private:
	//静态成员函数也是有访问权限的
	static void func2(){
		cout << "static void func2的调用" << endl;
	}

};

int Person::m_A = 0;

void test01(){
	//通过对象访问
	Person p;
	p.func();
	//通过类名访问
	Person::func();

	//Person::func2();类外无法访问私有的静态成员函数
}

int main(){

	test01();

	system("pause");
	return 0;
}
```


  > **参考**：黑马程序员匠心之作|C++教程从0到1入门编程,学习编程不再难
  > **链接**：[https://www.bilibili.com/video/BV1et411b73Z](https://www.bilibili.com/video/BV1et411b73Z)