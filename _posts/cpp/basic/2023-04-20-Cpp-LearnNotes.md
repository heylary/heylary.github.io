---
layout: original
title: "C++基础"
date: 2023-04-20 17:00:00 +0800
categories: C++学习
tag: C++
---
* content
{:toc}

# C/C++基础

## 1. 语言基础

### 1.c++语言的特点

1. C++在C语言基础上引入了**面对对象**的机制，同时也**兼容C语言**。

2. C++有**三大特性**（1）封装。（2）继承。（3）多态；

3. C++**更加安全**，增加了const常量、引用、四类cast转换（static_cast、dynamic_cast、const_cast、reinterpret_cast）、智能指针、try—catch等等

4. C++**可复用性**高，C++引入了**模板**的概念，后面在此基础上，实现了方便开发的**标准模板库STL**（Standard Template Library）

5. C++11中引入了nullptr、auto变量、Lambda匿名函数、右值引用、智能指针。

   

### 2. c语言和c++的区别

1. **c语言是c++的子集，c++能兼容c语言，但是c++又多了很多新特性**，如引用、智能指针、auto变量
2. c语言是**面向过程**的语言、c++是**面向对象**的语言
3. **c语言有很多不安全**的语言特性（如指针使用的危险，强制转换的不确定性、内存泄漏等），**c++更安全**（const常量、引用、cast转换、智能指针、try-catch）
4. c++有模板的概念、在此基础上开发了STL库



### 3. c++中struct和class的区别

1. 默认访问权限不一致，struct默认访问权限是public，class默认访问权限是private
2. 继承关系：struct公有继承，class私有继承
3. class可以用于定义模板参数，就像typename，struct不可以、



### 4. c++和c语言struct的区别

![image-20230310165321324](D:\WorkData\MarkdownData\StudyNotes\assets\image-20230310165321324.png)

使用时的区别：

C 中使用结构体需要加上 struct 关键字，或者对结构体使用 typedef 取别名，而 C++ 中可以省略 struct 关键字直接使用，例如：

1. 使用时的区别：C 中使用结构体需要加上 struct 关键字，或者对结构体使用 typedef 取别名，而 C++ 中可以省略 struct 关键字直接使用，例如：

   ```c
   struct Student{  
       int  iAgeNum;  string strName; 
   } 
   typedef struct Student Student2; //C中取别名  
   
   struct Student stu1; // C 中正常使用 
   Student2 stu2;   // C 中通过取别名的使用 
   Student stu3;   // C++ 中使用
   ```



### 5. C++编译时和C的区别

**参考回答**

1. **关键字：**在C++中，导入C函数的关键字是**extern**，表达形式为**extern “C”**， extern "C"的主要作用就是为了能够正确实现C++代码调用其他C语言代码。加上extern "C"后，会指示编译器这部分代码按**C语言**的进行编译，而不是C++的。
2. **编译区别：**由于C++支持**函数重载**，因此编译器编译函数的过程中会将函数的**参数类型**也加到编译后的代码中，而不仅仅是**函数名**；而C语言并不支持函数重载，因此编译C语言代码的函数时不会带上函数的参数类型，一般只包括**函数名**。

**答案解析**

```c
//extern示例 //在C++程序里边声明该函数，会指示编译器这部分代码按C语言的进行编译 
extern "C" int strcmp(const char *s1, const char *s2);  
```



### 6. C++如何从代码可执行二进制文件

  C++和C语言类似，一个C++程序从源码到执行文件，有四个过程，**预编译、编译、汇编、链接**。

1. 预编译，将注释、预编译指令等进行处理
2. 编译，进行词法分析，生成汇编代码
3. 汇编，将汇编代码转换成机器可以执行的指令
4. 链接，将不同源文件产生的目标文件进行链接、形成一个可执行文件

静态链接：在链接的时候把要调用的函数等链接到可执行文件，Window的后缀为.lib,Linux的后缀为.a

动态链接：在程序运行的时候再去找链接的函数，生成的可执行文件没有函数代码，只包含重定位信息。Window的后缀为.dll，Linux的后缀为.so



### 7. static的作用

静态变量与普通变量的最大差别在于**存储区域**不同。

定义一个**普通变量**时，它会被**分配到栈**（stack）上。而当我们定义一个**静态变量**时，它会被**分配到静态存储区**（static storage area）中，不随着函数调用的结束而销毁，而是**一直存在于内存**中。

静态变量有以下特点：

1. **生命周期长**：**静态变量的生命周期是整个程序运行期间**，即使所在的函数已经执行完毕，静态变量仍然存在于内存中；
2. **全局可见**：静态变量作用域为整个文件，因此在其所在的源文件中的任何地方都可以访问该变量；

- 当调用一个非静态成员函数时，**系统会将该对象的起始地址作为参数传递给该函数**，并将其保存在该函数的this指针中。

- **C++规定静态成员函数没有this指针**，它们不能通过this指针来访问任何对象的成员变量。相反，静态成员函数可以访问该类的静态成员变量以及其他静态成员函数。

总而言之，`static` 关键字可以用于定义静态变量或者静态函数，在程序运行期间始终存在，并具有特定的作用域和生命周期。



### 8. 数组和指针的区别

**概念**

1. 数组：存放多个相同数据类型的集合，数组名指向首元素的地址
2. 指针：存放的是变量在内存中的地址，指针名执行内存的首地址

**区别**

1. 赋值：同类型指针变量可以相互赋值，数组要一个元素一个元素赋值
2. 存储方式：数组在内存中是连续存放的，开辟一块连续的内存空间，指针指向地址空间的内存，空间不确定
3. 大小：数组所占空间的内存大小： sizeof(数组名)/sizeof(数据类型)



### 9. 什么是函数指针

函数指针是一个**指针，指向一个函数**

指针函数是一个**函数，返回一个指针**

```c++
#include <iostream>

// 定义一个函数指针类型
typedef int (*func_ptr_t)(int, int);

// 定义两个函数，分别用于加法和减法
int add(int a, int b) {
    return a + b;
}

int sub(int a, int b) {
    return a - b;
}

int main() {
    // 声明两个函数指针变量，分别指向add和sub函数
    func_ptr_t p_add = add;
    func_ptr_t p_sub = sub;

    // 调用函数指针所指向的函数
    std::cout << "3 + 4 = " << p_add(3, 4) << std::endl;
    std::cout << "3 - 4 = " << p_sub(3, 4) << std::endl;

    return 0;
}
```



```c++
#include <iostream>

// 定义一个指针函数，返回一个int类型的指针
int* create_int(int value) {
    int* p = new int(value);
    return p;
}

int main() {
    // 调用指针函数，返回一个指向动态分配变量的指针
    int* p = create_int(42);

    // 输出指针指向的值
    std::cout << *p << std::endl;

    // 释放动态分配的内存
    delete p;

    return 0;
}
```

### 10. 什么是野指针，产生和避免

**野指针是指指向非法内存地址的指针**。在C/C++程序中，野指针通常由以下两种情况产生：

1. **指针未初始化或已被释放**，则它的值就是一个不确定的、随机的内存地址。在这种情况下，使用指针会导致访问非法内存，从而产生野指针。

2. **指针操作越界**，如果一个指针变量指向了一个已经释放的内存空间或者超出了指针所指对象的范围，则使用该指针进行访问操作时也会产生野指针。

要避免野指针的产生，可以采取以下措施：

1. **初始化指针，如果无法确定合适的初始值，可以将指针初始化为**NULL或nullptr等特殊值**，以防止其成为野指针。

2. **及时释放指针**，在使用完毕后，应该及时释放指针指向的内存空间，避免出现“悬空指针”的情况。

3. **避免指针操作越界**，在进行指针操作时，应该小心谨慎，确保指针所指向的内存空间仍然是有效的，并且不会超出其所指对象的边界。

4. **使用智能指针**，使用智能指针可以大大减少野指针的出现。智能指针通过RAII（资源获取即初始化）技术来管理动态分配的内存空间，确保在对象生命周期结束时自动回收内存空间，从而避免了手动管理内存带来的风险。

总之，避免野指针的关键是要保证指针所指向的内存空间始终是有效的，并且能够正确地释放和管理内存空间。

1. 初始化置空
2. 释放后置空
3. 申请内存后判空

### 11. 静态局部变量、全局变量、局部变量的特点

**静态局部变量**

静态局部变量是指在**函数内部定义，但生命周期贯穿整个程序运行期间的变量**。它们与普通的局部变量不同，**只在函数第一次执行时初始化**，并且在整个程序运行期间保留其值。静态局部变量的使用场景包括需要在多次调用同一函数时保持数据的连续性，以及需要节省内存空间的情况。

**全局变量**

**全局变量是指在所有函数外部定义的变量，在整个程序运行期间都可以访问**。全局变量的生命周期通常与程序的运行周期相同，因此可以在程序的任何位置被访问和修改。全局变量的使用场景包括需要在不同的函数之间共享数据，以及需要在多个源文件中使用同一变量的情况。

**局部变量**

局部变量是指在函数内部定义的变量，其作用域仅限于函数内部。局部变量的生命周期始于函数被调用时开始，结束于函数执行完毕时结束。局部变量的使用场景包括需要在函数内部保存和处理临时数据的情况，以及需要限制变量作用范围的情况。



### 12. 内联函数和宏的区别

1. 内联函数是**编译期间**进行处理，而宏函数是**预编译期间**进行处理。
2. 内联函数在调用时会进行**参数类型检查和作用域检查**，而宏函数不会，可能会出现类型不匹配或者作用域问题导致的错误。
3. 内联函数是由**编译器处理**的，可以使用所有 C++ 的特性（如重载、虚函数等），而**宏函数只是简单的文本替换**，不能使用 C++ 的特性。
4. 内联函数的代码会复制到每个调用的地方，增加了代码量但可以**避免函数调用**的开销，而宏函数只是简单的文本替换，不会增加代码量，但也**没有避免函数调用的开销**。
5. 内联函数在编译时会进行类型检查等编译期间的优化，而宏函数则只是简单的文本替换，无法进行编译时优化。

因此，在可以使用内联函数的情况下，应该尽量使用内联函数，以提高程序的效率和可维护性。



### 13. i++和++i的区别

1. i++是先赋值后加、++i是先加后赋值
2. 后置++速度比较慢
3. i++不能作为左值，而++i可以作为左值
4. ++i前置递增运算符会将变量本身加1并返回该变量的引用，i++后置递增运算符返回的是变量原始的值



### 14. new 和 malloc的区别，底层实现原理

1. new是操作符，malloc是函数
2. new在调用时先分配内存，再调用构造函数，释放的会调用析构函数，而malloc没有构造函数和析构函数
3. malloc需要先申请内存大小，返回的指针需要强转，new会调用构造函数，不用指定内存大小
4. new可以被重载，malloc不可以

**malloc底层原理**

- 调用malloc时，先检查是否存在已分配但未使用的内存块，如果有直接返回内存卡
- 如果没有足够内存，当待分配的内存小于128KB时候调用brk函数拓展堆，当分配的内存大于128K时使用mmap()函数再进程地址空间映射一段新的虚拟内存，将它作为堆区。
- 初始化新申请的内存块，并加入内存池管理链表中，以便后续内存分配
- 当使用free的时候，会释放对应的内存块，并标记为未使用状态，将相应的内存段合并，以减少内存碎片

**new的底层原理**

1. 调用new在堆上分配一段大小足够内存
2. 调用对象的构造函数将内存中的数据初始化
3. 返回指向对象的指针



### 15.const的作用

1. 防止修改：const可以将变量定义为只读
2. 类型检查：const在编译期间进行类型检查，const指针不能指向非const对象
3. 优化代码：编译器会将const放入常量表中，提高效率
4. 支持重载：可以实现函数的重载



### 16. 常量指针和指针常量

左定值（常量指针），右定向（指针常量）

```
1. const int a;     //指的是a是一个常量，不允许修改。
2. const int *a;    //a指针所指向的内存里的值不变，即（*a）不变
3. int const *a;    //同const int *a;
4. int *const a;    //a指针所指向的内存地址不变，即a不变
5. const int *const a;   //都不变，即（*a）不变，a也不变
```



### 17.指针需要注意什么

1. 定义指针时，先初始化为NULL。
2. 用malloc或new申请内存之后，应该**立即检查**指针值是否为NULL。防止使用指针值为NULL的内存。
3. 不要忘记为数组和动态内存**赋初值**。防止将未被初始化的内存作为右值使用。
4. 避免数字或指针的下标**越界**，特别要当心发生“多1”或者“少1”操作
5. 动态内存的申请与释放必须配对，防止**内存泄漏**
6. 用free或delete释放了内存之后，立即将指针**设置为NULL**，防止“野指针”

**（1）初始化置NULL**

**（2）申请内存后判空**

**（3）指针释放后置NULL**



### 18. c++的几种传值方式

传参方式有这三种：**值传递、引用传递、指针传递**

1. 值传递：形参即使在函数体内值发生变化，也不会影响实参的值；
2. 引用传递：形参在函数体内值发生变化，会影响实参的值；
3. 指针传递：在指针指向没有发生改变的前提下，形参在函数体内值发生变化，会影响实参的值；



### 19. 左值、右值引用

在C++中，左值（lvalue）指的是一个具有名称、地址和可寻址性的对象，例如变量、数组、函数等；而右值（rvalue）则指的是一个临时的、无法被取地址的值，例如常量、字面量、表达式结果等。通常情况下，右值只能出现在赋值语句的右侧，例如：

```
Copy Codeint a = 1 + 2; // 1 + 2 是一个右值，赋值给变量a
```

C++11中引入了右值引用这个概念，并通过&&来标识。右值引用可以绑定到一个临时的、将要被销毁的对象上，例如函数返回值、临时对象等，从而实现对这些对象的高效移动或转移。

在vector<T>&& other中，other就是一个右值引用，它代表一个即将被销毁的vector对象，可以被移动或转移到另一个vector对象中。使用右值引用可以避免不必要的内存拷贝和资源释放，提高程序的性能和效率。

需要注意的是，使用右值引用时需要非常小心，以确保不会出现未定义行为。特别是在进行资源管理、多线程编程等场景下，需要格外注意右值引用的使用方式和规范。



## 2. C++内存

### 1. 堆和栈的区别

1. **内存的分配方式：**栈由编译器自动分配和释放，堆需要程序员手动分配和释放
2. **内存的管理方式：**栈采取先进先出的方式，堆没有固定顺序，可以随时分配和释放
3. **内存地址**：栈的变量存储在静态内存区，可以直接访问，堆的变量存储在动态内存区，地址不确定，需要指针来访问

### 2. C++的内存管理

​	在C++中，内存分为5个区，**堆、栈、自由存储区、静态存储区、常量存储区**

1. 堆：执行函数的时候，局部变量的都可以在栈上创建，在函数结束的时候自动被释放
2. 栈：调用new分配的内存块都在堆上，需要delete释放
3. 自由存储区：由malloc分配的内存块，需要free来结束自己的生命
4. 静态存储区：存储全局变量和静态变量
5. 常量存储区：存储常量，不允许被修改

### 3. 常见的内存错误及对策

1. 内存分配未成功，确实用了它
2. 内存分配成功，但没初始化时就引用了
3. 内存分配成功，但是操作越界
4. 忘记释放内存，内存泄漏
5. 释放内存，却继续使用

**对策：**

1. 定义指针，初始化为NULL
2. 调用malloc和New的时候，立刻检查指针值是否为NULL,防止使用指针为NULL的内存
3. 记得给数组和动态内存赋初值
4. 避免数字或指针的下标越界
5. 动态内存的申请和释放必须配对，防止内存泄漏
6. 用free和delete释放内存后，需要将指针置空
7. 使用智能指针

```c++
例如，在C语言中，可以使用如下代码进行指针检查：

c
int* ptr = (int*)malloc(sizeof(int));
if(ptr == NULL) {
    printf("Error: Memory allocation failed!\n");
    exit(1);
}
在C++语言中，可以使用如下代码进行指针检查：

c++
int* ptr = new int;
if(ptr == nullptr) {
    cout << "Error: Memory allocation failed!" << endl;
    exit(1);
}
```

### 4. 内存泄漏及解决方法

程序运行过程没有正确的释放不再使用的 志愿，导致系统内存浪费，最终可能导致系统崩溃

出现的原因：

1. new和malloc()申请内存后，没有使用delete和free()释放内存
2. 子类继承父类的时候，父类的析构函数不是虚函数

解决方法：

1. 检查代码，malloc()和free(),new和delete配对
2. 使用智能指针，它可以自动管理对象内存的生命周期，share_ptr可以共享多个对象，而unique_ptr只能共享一个对象

3. 使用RAII技术，它是一种资源获取即初始化，在构造函数中获取资源，在析构函数中释放资源
4. 使用内存池，它是一种分配机制，将内存分配的开销提前缓存起来，避免频繁的向操作系统申请和释放内存。



### 5. 一个程序有哪些section

从低地址到高地址：**代码段、数据段、BSS段、堆、共享区、栈等**

1. 代码段：存放执行代码的一块内存区域
2. 数据段：存放**初始化**的全局变量和静态变量的一块内存
3. BSS段：存放**未初始化**的全局变量和静态变量的一块内存
4. 程序运行时出现堆和栈:
   - 堆：动态申请内存时候的空间，从低地址向高地址增长
   - 栈：存储局部变量，从高地址向低地址增长
5. 共享区：存在堆和栈之间



### 5. 内存对齐

**编译器为结构体的每个成员按其自然边界（alignment）分配空间**，**即所谓的“对齐”，比如4字节的int型，其起始地址应该位于4字节的边界上，即起始地址能够被4整除**

需要字节对齐的根本原因在于CPU访问数据的效率问题



```c++
在C++中，数据类型的大小与所使用的操作系统和编译器有关。但是，通常情况下，在32位机器上，常用数据类型的大小如下：

char：1字节
bool：1字节
short：2字节
int：4字节
float：4字节
double：8字节
long double：12或16字节（取决于编译器）
unsigned char：1字节
unsigned int：4字节
unsigned short：2字节
long：4字节
unsigned long：4字节
而在64位机器上，常用数据类型的大小如下：

char：1字节
bool：1字节
short：2字节
int：4字节
float：4字节
double：8字节
long double：16字节
unsigned char：1字节
unsigned int：4字节
unsigned short：2字节
long：8字节
unsigned long：8字节
```



## 3. 面向对象

### 1. 什么是面向对象

将一切事务看作对象，这些对象拥有各自的属性和操作



### 2. 面向对象的三大特征

需要字节对齐的根本原因在于CPU访问数据的效率

**封装、继承、多态**

封装：将数据和操作数据的方法进行有机结合，隐藏对象的属性和实现细节，仅对外公开接口来和对象进行 交互

继承：可以使用现有类的所有功能。

多态：派生类重写基类方法，**基类引用指向派生类对象**，有重写和重载



### 3. 重写和重载

1. **重写**

   派生类存在重新定义的函数，所有参数类型一直，函数体不同，**被重写的函数必须是virtual类型**，c++会添加参数类型和返回类型作为**函数编译后的名称**

   纯虚函数：virtual void fun()=0。**即抽象类必须在子类实现这个函数**，即先有名称，没有内容，在派生类实现内容。

```c++
#include<bits/stdc++.h>  
using namespace std;  
class A { 
    public:  
    	virtual void fun()  {   cout << "A";  } 
}; 

class B :public A { 
    public:  
    	virtual void fun()  {   cout << "B";  } }; 

int main(void) {  
    A* a = new B();  
    a->fun();//输出B，A类中的fun在B类中重写 
}
```

2. **重载**

重载是在一个类中定义多个具有相同名称但参数列表不同的函数

```c++
#include<bits/stdc++.h>  
using namespace std;  
class A {  
    void fun() {};  
    void fun(int i) {};  
    void fun(int i, int j) {};     
    void fun1(int i,int j) {}; 
};
```

语言实现函数重载

1. 使用函数指针来实现，重载的函数不能使用同名称，只是类似的实现了函数重载功能
2. 重载函数使用可变参数，方式如打开文件open函数
3. gcc有内置函数，程序使用编译函数可以实现函数重载

示例如下：

```c
#include<stdio.h>   
void func_int(void * a) {     
    printf("%d\n",*(int*)a);  //输出int类型，注意 void * 转化为int 
}   

void func_double(void * b) {     
    printf("%.2f\n",*(double*)b); 
}   

typedef void (*ptr)(void *);  //typedef申明一个函数指针  
void c_func(ptr p,void *param) {      
    p(param);                //调用对应函数 
}   

int main() {     
    int a = 23;     
    double b = 23.23;     
    c_func(func_int,&a);     
    c_func(func_double,&b);     
    return 0; 
}
```



### 4. 构造函数有几种，作用是什么

1. **默认构造函数**
2. **初始化构造函数**

在定义类的对象的时候，完成对象的初始化工作。

1. 默认构造函数和初始化构造函数。 在定义类的对象的时候，完成对象的初始化工作。

   ```c
   class Student { 
    public:  //默认构造函数  
    	Student()  {     
        		num=1001;        
        		age=18;      
           }  
       //初始化构造函数  
       Student(int n,int a):num(n),age(a){} 
       
    private:  
       int num;  
       int age; }; 
   
   int main() {  
       //用默认构造函数初始化对象S1  
       Student s1;  
       //用初始化构造函数初始化对象S2  
       Student s2(1002,18); 
      return 0; }
   ```

   

3. **拷贝构造函数**

   拷贝构造函数用于复制本类的对象

   ```c
   #include "stdafx.h" 
   #include "iostream.h"  
   class Test {     
       int i;     
       int *p; 
     public:     
       Test(int ai,int value)     {         
           i = ai;         
           p = new int(value);     
       }     
       
       ~Test()     { 
           delete p;     
       }     
       
       Test(const Test& t)     {
           this->i = t.i;         
           this->p = new int(*t.p);     
       } 
   }; //复制构造函数用于复制本类的对象 
   
   int main(int argc, char* argv[]) {
       Test t1(1,2);     
       Test t2(t1);//将对象t1复制给t2。注意复制和赋值的概念不同     
      	return 0; 
   }
   ```

   赋值构造函数默认实现的是值拷贝（浅拷贝）。

4. **移动构造函数**

**用于将其他类型的变量，隐式转换为本类对象**

在创建对象时用于将一个已存在的对象作为参数传入，从而创建一个新的对象并将其内容与原始对象相同



### 5. 向上转型和向下转型

1. 子类转换为父类：向上转型，这种转换相对来说比较安全不会有数据的丢失；
2. 父类转换为子类：向下转型，可以使用强制转换，这种转换时不安全的，会导致数据的丢失，使用dynamic_cast<type_id>(expression)原因是父类的指针或者引用的内存中可能不包含子类的成员的内存。

```c++
#include <iostream>

using namespace std;

class Animal {
public:
    virtual void speak() {
        cout << "I am an animal." << endl;
    }
};

class Dog : public Animal {
public:
    void speak() {
        cout << "I am a dog." << endl;
    }

    void bark() {
        cout << "Woof! Woof!" << endl;
    }
};

int main() {
    Animal* animal_ptr = new Dog(); // 向上转型
    animal_ptr->speak(); // 输出：I am a dog.
    
    Dog* dog_ptr = dynamic_cast<Dog*>(animal_ptr); // 向下转型
    if (dog_ptr) {
        dog_ptr->bark(); // 输出：Woof! Woof!
    }
    
    delete animal_ptr;
    return 0;
}
```

### 6. 深拷贝和浅拷贝，如何实现深拷贝

深拷贝和浅拷贝是指在进行对象复制时，是否复制对象的所有成员变量。

**浅拷贝只复制对象的所有成员变量的值，而不复制指针所指向的内存；深拷贝则会复制指针所指向的内存**

深拷贝会完全拷贝对象以及所有子对象，两个是独立的对象

1. 浅拷贝：又称值拷贝，**将源对象的值拷贝到目标对象中去**，本质上来说源对象和目标对象**共用一份实体**，只是所引用的变量名不同，**地址其实还是相同**的。举个简单的例子，你的小名叫西西，大名叫冬冬，当别人叫你西西或者冬冬的时候你都会答应，这两个名字虽然不相同，但是都指的是你。

2. 深拷贝，**拷贝的时候先开辟出和源对象大小一样的空间，然后将源对象里的内容拷贝到目标对象中去**，这样两个指针就指向了不同的内存位置。并且里面的内容是一样的，这样不但达到了我们想要的目的，还不会出现问题，两个指针先后去调用析构函数，分别释放自己所指向的位置。即为每次增加一个指针，便申请一块新的内存，并让这个指针指向新的内存，**深拷贝情况下，不会出现重复释放同一块内存的错误**。

3. 深拷贝的实现：深拷贝的拷贝构造函数和赋值运算符的重载传统实现：

   ```c
   STRING( const STRING& s )
   {
       //_str = s._str;
       _str = new char[strlen(s._str) + 1];
       strcpy_s( _str, strlen(s._str) + 1, s._str );
   }
   STRING& operator=(const STRING& s)
   {
       if (this != &s)
       {
           //this->_str = s._str;
           delete[] _str;
           this->_str = new char[strlen(s._str) + 1];
           strcpy_s(this->_str, strlen(s._str) + 1, s._str);
       }
       return *this;
   }
   ```



```c++
浅拷贝
class Person {
public:
    char* name;
    int age;

    Person(const char* n, int a) {
        name = new char[strlen(n) + 1];
        strcpy(name, n);
        age = a;
    }

    Person(const Person& other) {
        name = other.name;
        age = other.age;
    }

    ~Person() {
        delete[] name;
    }
};

int main() {
    Person p1("Alice", 20);
    Person p2 = p1; // 浅拷贝
    p2.name[0] = 'B';
    cout << p1.name << endl; // 输出 "Blice"
    return 0;
}

```

```c++
深拷贝
class Person {
public:
    char* name;
    int age;

    Person(const char* n, int a) {
        name = new char[strlen(n) + 1];
        strcpy(name, n);
        age = a;
    }

    Person(const Person& other) {
        name = new char[strlen(other.name) + 1];
        strcpy(name, other.name);
        age = other.age;
    }

    ~Person() {
        delete[] name;
    }
};

int main() {
    Person p1("Alice", 20);
    Person p2 = p1; // 深拷贝
    p2.name[0] = 'B';
    cout << p1.name << endl; // 输出 "Alice"
    cout << p2.name << endl; // 输出 "Blice"
    return 0;
}


```



### 7. 虚析构函数

虚析构：将**可能会被继承的父类的析构函数设置为虚函数**，可以保证当我们new一个子类，然后使用**基类指针指向该子类对象**，释放基类指针时可以释放掉子类的空间，**防止内存泄漏**。如果基类的析构函数不是虚函数，在特定情况下会导致派生来无法被析构。

1. 用派生类类型指针绑定派生类实例，析构的时候，不管基类析构函数是不是虚函数，都会正常析构
2. 用基类类型指针绑定派生类实例，析构的时候，如果基类析构函数不是虚函数，则只会析构基类，不会析构派生类对象，从而造成内存泄漏。为什么会出现这种现象呢，个人认为析构的时候如果没有虚函数的动态绑定功能，就只根据指针的类型来进行的，而不是根据指针绑定的对象来进行，所以只是调用了基类的析构函数；如果基类的析构函数是虚函数，则析构的时候就要根据指针绑定的对象来调用对应的析构函数了。

C++默认的析构函数不是虚函数是因为虚函数需要额外的虚函数表和虚表指针，占用额外的内存。而对于不会被继承的类来说，其析构函数如果是虚函数，就会浪费内存。因此C++默认的析构函数不是虚函数，而是只有当需要当作父类时，设置为虚函数。

不能虚构造：

1. 从存储空间角度：虚函数对应一个vtale,这个表的地址是存储在对象的内存空间的。如果将构造函数设置为虚函数，就需要到vtable 中调用，可是对象还没有实例化，没有内存空间分配，如何调用。（悖论）
2. 从使用角度：虚函数主要用于在信息不全的情况下，能使重载的函数得到对应的调用。构造函数本身就是要初始化实例，那使用虚函数也没有实际意义呀。所以构造函数没有必要是虚函数。虚函数的作用在于通过父类的指针或者引用来调用它的时候能够变成调用子类的那个成员函数。而构造函数是在创建对象时自动调用的，不可能通过父类的指针或者引用去调用，因此也就规定构造函数不能是虚函数。
3. 从实现上看，**vbtl 在构造函数调用后才建立**，因而构造函数不可能成为虚函数。从实际含义上看，在调用构造函数时还不能确定对象的真实类型（因为子类会调父类的构造函数）；而且构造函数的作用是提供初始化，在对象生命期只执行一次，不是对象的动态行为，也没有太大的必要成为虚函数。



### 8. 虚函数和纯虚函数的作用

1. 含有纯虚函数的类被称为抽象类，而只含有虚函数的类不能被称为抽象类。

2. 虚函数可以被直接使用，也可以被子类重载以后，以多态的形式调用，而纯虚函数必须在子类中实现该函数才可以使用，因为纯虚函数在基类有声明而没有定义。

3. 虚函数和纯虚函数都可以在子类中被重载，以多态的形式被调用



### 9. 拷贝构造函数和赋值构造函数

拷贝构造函数和赋值构造函数都是用于对象的复制。它们的区别在于：

- **拷贝构造函数是在创建一个新对象时调用**的，它将一个已经存在的对象作为参数，并使用该对象的值来初始化新对象。拷贝构造函数的原型通常是

  ClassName(const ClassName& other)

  。

- **赋值构造函数是在已经存在的对象上调用**的，它将一个已经存在的对象的值赋给另一个已经存在的对象。赋值构造函数的原型通常是

  ClassName& operator=(const ClassName& other)

  。

因此，拷贝构造函数和赋值构造函数的主要区别在于它们的调用时机和用途。拷贝构造函数用于创建新对象，而赋值构造函数用于将一个对象的值赋给另一个对象。



### 10. 什么是仿函数，作用

在C++中，仿函数是一种重载了函数调用运算符()的类，它可以像函数一样被调用。仿函数可以看作是一种特殊的函数对象，它可以保存状态，可以作为参数传递给其他函数，也可以作为返回值返回给其他函数。

仿函数的作用主要有以下几个方面：

1. 仿函数可以作为STL算法的参数，用于指定算法的具体操作。例如，STL中的sort算法可以接受一个仿函数作为参数，用于指定排序的方式。
2. 仿函数可以用于封装一些特定的操作，使得代码更加简洁和易于维护。例如，我们可以定义一个仿函数来判断一个字符串是否是数字，然后在其他函数中使用这个仿函数来进行判断。
3. 仿函数可以保存状态，因此可以用于实现一些需要保存状态的操作。例如，我们可以定义一个仿函数来计算一个数的平方，然后在其他函数中多次调用这个仿函数来计算不同数的平方。

总之，仿函数是一种非常有用的C++特性，它可以使代码更加灵活和可复用。

```c++
class StringLengthCompare {
public:
    bool operator()(const string& s1, const string& s2) const {
        return s1.length() < s2.length();
    }
};
```



### 11. 哪些函数不能被声明为虚函数

**参考回答**

常见的不不能声明为虚函数的有：普通函数（非成员函数），静态成员函数，内联成员函数，构造函数，友元函数。

1. 为什么C++不支持普通函数为虚函数？

   普通函数（非成员函数）只能被overload，不能被override，声明为虚函数也没有什么意思，因此编译器会在编译时绑定函数。

1. 为什么C++不支持构造函数为虚函数？

   这个原因很简单，主要是从语义上考虑，所以不支持。因为构造函数本来就是为了明确初始化对象成员才产生的，然而virtual function主要是为了再不完全了解细节的情况下也能正确处理对象。另外，virtual函数是在不同类型的对象产生不同的动作，现在对象还没有产生，如何使用virtual函数来完成你想完成的动作。（这不就是典型的悖论）

   构造函数用来创建一个新的对象,而虚函数的运行是建立在对象的基础上,在构造函数执行时,对象尚未形成,所以不能将构造函数定义为虚函数

2. 为什么C++不支持内联成员函数为虚函数？

   其实很简单，那内联函数就是为了在代码中直接展开，减少函数调用花费的代价，虚函数是为了在继承后对象能够准确的执行自己的动作，这是不可能统一的。（再说了，*inline函数在编译时被展开，虚函数在运行时才能动态的绑定函数*）

   内联函数是在编译时期展开,而虚函数的特性是运行时才动态联编,所以两者矛盾,不能定义内联函数为虚函数

3. 为什么C++不支持静态成员函数为虚函数？

   这也很简单，静态成员函数对于每个类来说只有一份代码，所有的对象都共享这一份代码，他也没有要动态绑定的必要性。

   静态成员函数属于一个类而非某一对象,没有this指针,它无法进行对象的判别

4. 为什么C++不支持友元函数为虚函数？

   因为C++不支持友元函数的继承，对于没有继承特性的函数没有虚函数的说法。

###  12. 类模板和模板类的区别

**类模板是一种通用的类定义**，它可以用于创建多个不同类型的类。类模板的定义以关键字template开头，后面跟着一个或多个模板参数，用于指定类模板的类型参数

**模板类是通过类模板实例化得到的一个具体的类**

```c++
template <typename T> //类模板
class MyVector {
public:
    MyVector(int size) {
        data = new T[size];
        this->size = size;
    }

    ~MyVector() {
        delete[] data;
    }

    T& operator[](int index) {
        return data[index];
    }

private:
    T* data;
    int size;
};

int main() {
    MyVector<int> v(10);
    for (int i = 0; i < 10; i++) {
        v[i] = i;
    }
    for (int i = 0; i < 10; i


```



## 4. STL

### 1. STL 的基本组成部分

标准模板库（Standard Template Library,简称STL）简单说，就是一些常用数据结构和算法的模板的集合。

  **广义上讲**，STL分为3类：Algorithm（算法）、Container（容器）和Iterator（迭代器），容器和算法通过迭代器可以进行无缝地连接。

  **详细的说**，STL由6部分组成：容器(Container)、算法（Algorithm）、 迭代器（Iterator）、仿函数（Function object）、适配器（Adaptor）、空间配制器（Allocator）。

  标准模板库STL主要由6大组成部分：

1. 容器(Container)  

     是一种数据结构， 如list, vector, 和deques，以模板类的方法提供。为了访问容器中的数据，可以使用由容器类输出的迭代器。

2. 算法（Algorithm）

     是用来操作容器中的数据的模板函数。例如，STL用sort()来对一 个vector中的数据进行排序，用find()来搜索一个list中的对象， 函数本身与他们操作的数据的结构和类型无关，因此他们可以用于从简单数组到高度复杂容器的任何数据结构上。

3. 迭代器（Iterator）

     提供了访问容器中对象的方法。例如，可以使用一对迭代器指定list或vector中的一定范围的对象。 迭代器就如同一个指针。事实上，C++ 的指针也是一种迭代器。 但是，迭代器也可以是那些定义了operator*()以及其他类似于指针的操作符方法的类对象;

4. 仿函数（Function object）

     仿函数又称之为函数对象， 其实就是重载了操作符的struct,没有什么特别的地方。

5. 适配器（Adaptor）

     简单的说就是一种接口类，专门用来修改现有类的接口，提供一中新的接口；或调用现有的函数来实现所需要的功能。主要包括3中适配器Container Adaptor、Iterator Adaptor、Function Adaptor。

6. 空间配制器（Allocator）

     为STL提供空间配置的系统。其中主要工作包括两部分：

   （1）对象的创建与销毁；

   （2）内存的获取与释放。

### 2.  STL 中常见的容器，并介绍一下实现原理

 容器可以用于存放各种类型的数据（基本类型的变量，对象等）的数据结构，都是**模板类**

分为**顺序容器、关联式容器、容器适配器**三种类型，三种类型容器特性分别如下：

1. 顺序容器

     容器并非排序的，元素的插入位置同元素的值无关。包含vector、deque、list，具体实现原理如下：

   （1）vector  头文件<vector>

   ​      动态数组。元素在内存连续存放。随机存取任何元素都能在常数时间完成。在尾端增删元素具有较佳的性能。

   （2）deque  头文件<deque>

     双向队列。元素在内存连续存放。随机存取任何元素都能在常数时间完成（仅次于vector）。在两端增删元素具有较佳的性能（大部分情况下是常数时间）。

   （3）list  头文件<list>

      双向链表。元素在内存不连续存放。在任何位置增删元素都能在常数时间完成。不支持随机存取。

2. 关联式容器

     元素是排序的；插入任何元素，都按相应的排序规则来确定其位置；在查找时具有非常好的性能；通常以平衡二叉树的方式实现。包含set、multiset、map、multimap，具体实现原理如下：

   （1）set/multiset  头文件<set>

   ​    set 即集合。set中不允许相同元素，multiset中允许存在相同元素。

   （2）map/multimap  头文件<map>

   ​    map与set的不同在于map中存放的元素有且仅有两个成员变，一个名为first,另一个名为second, map根据first值对元素从小到大排序，并可快速地根据first来检索元素。

     **注意：**map同multimap的不同在于是否允许相同first值的元素。

3. 容器适配器

     封装了一些基本的容器，使之具备了新的函数功能，比如把deque封装一下变为一个具有stack功能的数据结构。这新得到的数据结构就叫适配器。包含stack,queue,priority_queue，具体实现原理如下：

   （1）stack  头文件<stack>

   ​    栈是项的有限序列，并满足序列中被删除、检索和修改的项只能是最进插入序列的项（栈顶的项）。后进先出。

   （2）queue  头文件<queue>

   ​    队列。插入只可以在尾部进行，删除、检索和修改只允许从头部进行。先进先出。

   （3）priority_queue  头文件<queue>

   ​    优先级队列。内部维持某种有序，然后确保优先级最高的元素总是位于头部。最高优先级元素总是第一个出列。

### 3.   map、 hashtable、deque、list 的实现原理

map、hashtable、deque、list实现机理分别是红黑树、函数映射、双向队列、双向链表

**1. map**

map内部实现了一个**红黑树**（红黑树是非严格平衡的二叉搜索树，而AVL是严格平衡二叉搜索树），红黑树有自动排序的功能，因此map内部所有元素都是有序的，红黑树的每一个节点都代表着map的一个元素。因此，对于map进行的查找、删除、添加等一系列的操作都相当于是对红黑树进行的操作。map中的元素是按照二叉树（又名二叉查找树、二叉排序树）存储的，特点就是左子树上所有节点的键值都小于根节点的键值，右子树所有节点的键值都大于根节点的键值。使用中序遍历可将键值按照从小到大遍历出来。

**2. hashtable**

  hashtable采用了**函数映射的思想**记录的存储位置与记录的关键字关联起来，从而能够很快速地进行查找。这决定了哈希表特殊的数据结构，它同数组、链表以及二叉排序树等相比较有很明显的区别，它能够快速定位到想要查找的记录，而不是与表中存在的记录的关键字进行比较来进行查找。

**3. deque**

 deque内部实现的是一个**双向队列**。元素在内存连续存放。随机存取任何元素都在常数时间完成（仅次于vector）。所有适用于vector的操作都适用于deque。在两端增删元素具有较佳的性能（大部分情况下是常数时间）。

**4. list**

  list内部实现的是一个**双向链表**。元素在内存不连续存放。在任何位置增删元素都能在常数时间完成。不支持随机存取。无成员函数，给定一个下标i，访问第i个元素的内容，只能从头部挨个遍历到第i个元素。



### 4. STL 的空间配置器

STL（标准模板库）的空间配置器（allocator）是一种用于管理内存分配和释放的组件。

STL的空间配置器主要有两个目的：

1. **为了提高内存分配效率，避免频繁地调用系统函数 malloc 和 free。**
2. 为了更好地支持 STL 容器中的对象构造、析构和重分配等操作。

STL的空间配置器在分配一块内存时，会先从自己的内存池（memory pool）中寻找可用的内存块。如果内存池中没有足够的内存块，则会向系统申请一块较大的内存作为新的内存池，并将其划分成多个小块。每一个小块都可以用来分配单个对象或者连续的对象序列。

在内存释放时，空间配置器会将内存块归还给对应的内存池，以便下次再次使用。这样就能减少频繁地调用系统函数 malloc 和 free，提高内存分配的效率。

STL的空间配置器是一个泛型类，支持各种数据类型的内存分配和释放。常用的 STL容器，比如 vector、list、map 等都使用了空间配置器来管理内存的分配和释放。

STL的空间配置器一般是通过以下两个部分来实现的：

1. 内存池（memory pool）：内存池是一个预先分配好的内存块，用于管理对象的分配和释放。内存池中维护了一个指向可用内存块的指针和一个指向已使用内存块的指针，可以快速地将内存块分配给对象，并在其生命周期结束后将其归还给内存池。
2. 分配器（allocator）：分配器是一个泛型类，**提供了 alloc 和 dealloc 两个静态成员函数，用于对内存进行分配和释放**。在分配内存时，分配器会先从内存池中寻找可用的内存块，如果内存池中没有可用内存块，则会重新申请一块内存作为新的内存池，并将其划分成多个小块。在释放内存时，分配器会将内存块归还给对应的内存池。

STL的各种容器都有自己的默认空间配置器，但也允许用户自定义空间配置器。用户可以通过**重载分配器的 alloc 和 dealloc 函数来实现自己的空间配置器。**



### 5. STL的容器有哪些、查找的空间复杂度

STL中常用的容器有**vector、deque（增删）、list（查）**、map、set、multimap、multiset、**unordered_map、unordered_se**t等。容器底层实现方式及时间复杂度分别如下：

1. vector
   - 采用一维数组实现、元素在内存中连续存放
     - 插入 O（N）
     - 查看 O（1）
     - 删除 O（N）
2. deque
   - 采用双向队列实现、元素在内存中连续存放
     - 插入 O（N）
     - 查看 O（1）
     - 删除 O（N）

3. list

   - 采用双向链表实现，元素存放在堆中，不同操作的时间复杂度为：

     - 插入: O(1)

     - 查看: O(N)

     - 删除: O(1)

4. map、set、multimap、multiset

   - 上述四种容器采用红黑树实现，红黑树是平衡二叉树的一种。不同操作的时间复杂度近似为:

     - 插入: O(logN)

     - 查看: O(logN)

     - 删除: O(logN)

5. unordered_map、unordered_set、unordered_multimap、 unordered_multiset

   - 上述四种容器采用哈希表实现，不同操作的时间复杂度为： 插入: O(1)，最坏情况O(N)

     - 查看: O(1)，最坏情况O(N)

     - 删除: O(1)，最坏情况O(N)



### 6. 迭代器用过吗？什么时候会失效？

  Iterator类的访问方式就是把不同集合类的访问逻辑抽象出来，使得**不用暴露集合内部的结构而达到循环遍历集合**的效果

1. 数据结构是连续存储的数组时候进行增删操作就会。在使用vector、deque等容器时，如果对其中的元素进行了添加、删除操作，会导致所有指向该容器后面位置的迭代器都失效。

2. 同时，C++11中新增了一些更加安全的迭代器类型，比如const_iterator和move_iterator，它们能够减少迭代器失效的可能性。

```c++
//在C++11中，引入了两种新的迭代器类型：const_iterator和move_iterator。

const_iterator
const_iterator是一个只读迭代器，它只能读取容器中的元素，不能修改它们。使用const_iterator可以避免因为意外的修改而导致程序崩溃的情况。例如：

std::vector<int> v = {1, 2, 3};
std::vector<int>::const_iterator it = v.begin();
*it = 4; // 编译错误，const_iterator只读
move_iterator
move_iterator是一个移动迭代器，它用于移动容器中的元素。move_iterator通常与std::move配合使用，可以对容器中的元素进行移动语义。例如：

std::vector<std::string> src = {"hello", "world"};
std::vector<std::string> dest;
std::move(src.begin(), src.end(), std::back_inserter(dest));
//上述代码将src中的元素移动到dest中，而不是拷贝。这样做可以避免不必要的内存分配和数据拷贝。

//需要注意的是，由于move_iterator的特殊性质，使用它可能会导致迭代器失效。因此，在使用move_iterator时需要仔细考虑容器的修改操作，以避免出现不可预期的行为。
```



### 7. STL迭代器是怎么删除元素的

STL迭代器提供了两种删除元素的方式，分别是erase()和remove()。

erase()函数可以通过传递迭代器位置来删除指定元素。它接受一个迭代器参数，该迭代器指向要删除的元素。例如，在vector容器中删除第5个元素，可以使用以下代码：

```c++
Copy Codestd::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.begin() + 4; //指向第5个元素
v.erase(it); //删除第5个元素
```

注意，erase()函数会改变容器大小，并且会使迭代器失效。

remove()函数则是通过值来删除元素。它接受两个参数：要删除的值和指向容器首元素的迭代器。它会从容器中删除所有等于要删除的值的元素，并返回指向新的末尾位置的迭代器。例如，在vector容器中删除所有等于3的元素，可以使用以下代码：

```c++
Copy Codestd::vector<int> v = {1, 2, 3, 4, 5};
auto new_end = std::remove(v.begin(), v.end(), 3); //删除所有等于3的元素
v.erase(new_end, v.end()); //擦除新的末尾位置到容器结尾的元素
```

这里需要注意的是，remove()函数并没有真正地删除元素，而是将要删除的元素移到了容器尾部，因此需要使用erase()函数来擦除移动后的元素。

### 8. STL 中 resize 和 reserve 的区别

1. 在 C++ STL 中，`resize()` 和 `reserve()` 是两个可以用来管理容器大小的函数。

   `resize()` 函数改变容器中的元素数量，如果新的大小小于当前大小，则容器中的元素被截断。如果新的大小大于当前大小，则新添加的元素将使用默认值进行初始化。例如，对于 `vector` 容器来说，`resize()` 可以用来增加或减少容器中元素的数量。

   

   而 `reserve()` 函数只分配内存空间，但并不改变容器中实际元素的数量，也不会构造任何元素。它仅仅是为容器预留足够的内存空间，以便在之后的操作中可以更高效地进行插入或添加操作。因此，当需要向容器中添加大量元素时，先调用 `reserve()` 函数可以避免反复重新分配内存空间，从而提高程序效率。

   总之，**`resize()` 改变容器中的元素数量，而 `reserve()` 仅仅预留内存空间。**



### 9. map和unordered_map的区别，底层实现

map 和 unordered_map 是 C++ STL 中的两种关联容器，它们都用于存储键值对，并支持按照键（key）快速查找对应值（value），但它们的实现方式有所不同。

**map 使用红黑树实现**，因此它的元素默认是按照键值大小升序排序的。由于红黑树的高度平衡，因此查找、插入和删除操作的时间复杂度都是 O(log n) 级别的。另外，map 还支持自定义比较函数，可以自定义键的排序规则。

**unordered_map 使用哈希表实现**，因此它的元素并不会按照键值大小排序，而是**根据键值的哈希值分布来组织存储**。哈希表的优势在于能够实现常数级别的查找、插入和删除操作（即 O(1)），但是在处理冲突等方面需要额外的开销。另外，为了避免哈希冲突，unordered_map 需要指定一个哈希函数。

总的来说，map 适合于元素有序、查询频繁的场景；而 unordered_map 适合于元素无序、插入与删除频繁、查询相对较少的场景。



### 10. vector的实现原理

  vector底层实现原理为**一维数组**（元素在空间连续存放）。

1. 新增元素

   vector的insert操作可以在任意位置插入一个元素，由于vector使用连续的内存空间存储元素，因此在执行insert操作时需要确保所有元素都能够顺利地向后移动以腾出空间。具体实现步骤如下：

   判断vector当前是否已满，如果满了则需要扩展容量，以便能够插入新的元素。

   找到要插入的位置，即指定的迭代器所在的位置。

   从插入位置开始，将之后的所有元素都向后移动一个位置，为新元素腾出空间。

   在指定位置上存入新元素，并增加vector的元素数量。

   下面是一个简单的insert函数的实现示例：

   ```c++
   void insert(iterator position, const T& val) {
       // 判断是否需要扩展容量
       if (size() == capacity()) {
           reserve(size() + 1);
       }
       
       // 计算插入位置对应的索引
       size_t index = position - begin();
       
       // 将插入位置后面的元素都向后移动一个位置
       for (size_t i = size(); i > index; --i) {
           *(begin() + i) = *(begin() + i - 1);
       }
       
       // 在指定位置上存入新元素，并增加元素数目
       *(begin() + index) = val;
       ++m_size;
   }
   ```

```c++
template <typename T>
class vector {
public:
    typedef T* iterator;
    typedef const T* const_iterator;

    vector() : m_size(0), m_capacity(0), m_data(nullptr) {}

    vector(size_t n, const T& val = T())
        : m_size(n), m_capacity(n), m_data(new T[n])
    {
        for (size_t i = 0; i < n; ++i)
            m_data[i] = val;
    }

    // 拷贝构造函数
    vector(const vector<T>& other) : m_size(other.m_size), m_capacity(other.m_capacity), m_data(new T[other.m_capacity])
    {
        for (size_t i = 0; i < m_size; ++i)
            m_data[i] = other[i];
    }

    // 移动构造函数
    vector(vector<T>&& other) noexcept : m_size(other.m_size), m_capacity(other.m_capacity), m_data(other.m_data)
    {
        other.m_size = 0;
        other.m_capacity = 0;
        other.m_data = nullptr;
    }

    // 析构函数
    ~vector() { delete[] m_data; }

    // 复制赋值运算符
    vector<T>& operator=(const vector<T>& other)
    {
        if (this != &other) {
            delete[] m_data;
            m_size = other.m_size;
            m_capacity = other.m_capacity;
            m_data = new T[m_capacity];
            for (size_t i = 0; i < m_size; ++i)
                m_data[i] = other[i];
        }
        return *this;
    }

    // 移动赋值运算符
    vector<T>& operator=(vector<T>&& other) noexcept
    {
        if (this != &other) {
            delete[] m_data;
            m_size = other.m_size;
            m_capacity = other.m_capacity;
            m_data = other.m_data;
            other.m_size = 0;
            other.m_capacity = 0;
            other.m_data = nullptr;
        }
        return *this;
    }

    size_t size() const { return m_size; }

    bool empty() const { return m_size == 0; }

    size_t capacity() const { return m_capacity; }

    T& operator[](size_t index) { return m_data[index]; }

    const T& operator[](size_t index) const { return m_data[index]; }

    void push_back(const T& val)
    {
        if (m_size == m_capacity)
            reserve(m_capacity == 0 ? 1 : m_capacity * 2);
        m_data[m_size++] = val;
    }

    void pop_back()
    {
        if (!empty())
            --m_size;
    }

    iterator begin() { return m_data; }

    const_iterator begin() const { return m_data; }

    iterator end() { return m_data + m_size; }

    const_iterator end() const { return m_data + m_size; }

    void reserve(size_t new_cap)
    {
        if (new_cap > m_capacity) {
            T* new_data = new T[new_cap];
            for (size_t i = 0; i < m_size; ++i)
                new_data[i] = m_data[i];
            delete[] m_data;
            m_data = new_data;
            m_capacity = new_cap;
        }
    }

    void resize(size_t new_size)
    {
        if (new_size > m_size)
            reserve(new_size);
        while (m_size < new_size)
            m_data[m_size++] = T();
        m_size = new_size;
    }

    void clear() { m_size = 0; }

    iterator erase(iterator position)
    {
        if (position >= begin() && position < end()) {
            for (iterator i = position + 1; i != end(); ++i)
                *(i - 1) = *i;
            --m_size;
        }
        return position;
    }

    iterator insert(iterator position, const T& val)
    {
        size_t index = position - begin();
        if (m_size == m_capacity)
            reserve(m_capacity == 0 ? 1 : m_capacity * 2);
        for (iterator i = end(); i != begin() + index; --i)
            *i = *(i - 1);
        m_data[index] = val;
        ++m_size;
        return begin() + index;
    }

private:
    size_t m_size;
    size_t m_capacity;
    T* m_data;
};

```



### 11. push_back()和emplace_back()的区别

`push_back`是STL中用于在vector、deque等容器的末尾添加元素的函数，它将**构造一个临时对象，然后使用拷贝构造函数把这个临时对象放入容器中**。由于需要构造和销毁临时对象，因此`push_back`的效率相对较低。

`emplace_back`是C++11新增的函数，也用于在vector、deque等容器的末尾添加元素。它与`push_back`的区别在于，`emplace_back`**不会构造临时对象，而是直接在容器内部构造新对象**，因此效率更高，同时也避免了不必要的对象拷贝。`emplace_back`的参数列表可以直接传递给元素类型的构造函数。



## 5. C++11新特性

### 1. 增加了哪些新特性

C++新特性主要包括包含语法改进和标准库扩充两个方面，主要包括以下11点：

1. 语法的改进

   （1）统一的初始化方法

   （2）成员变量默认初始化

   （3）auto关键字  用于定义变量，编译器可以自动判断的类型（前提：定义一个变量时对其进行初始化）

   （4）decltype  求表达式的类型

   （5）智能指针 shared_ptr

   （6）空指针 nullptr（原来NULL）

   （7）基于范围的for循环

   （8）右值引用和move语义  让程序员有意识减少进行深拷贝操作

2. 标准库扩充（往STL里新加进一些模板类，比较好用）

   （9）无序容器（哈希表）  用法和功能同map一模一样，区别在于哈希表的效率更高

   （10）正则表达式  可以认为正则表达式实质上是一个字符串，该字符串描述了一种特定模式的字符串

   （11）Lambda表达式

   

#### **1. 统一的初始化方法**

C++98/03 可以使用初始化列表（initializer list）进行初始化：

```c++
int i_arr[3] = { 1, 2, 3 }; 
long l_arr[] = { 1, 3, 2, 4 }; 
struct A {     
	int x;     int y; 
} 
a = { 1, 2 };
```

  **但是**这种初始化方式的**适用性非常狭窄**，只有上面提到的这两种数据类型可以使用初始化列表。在 C++11 中，初始化列表的适用性被大大增加了。它现在可以用于任何类型对象的初始化，实例如下：

```c++
class Foo { 
	public:     
	Foo(int) {} 
private:     
	Foo(const Foo &); 
}; 
int main(void) {     
	Foo a1(123);     
	Foo a2 = 123;  //error: 'Foo::Foo(const Foo &)' is private     
	Foo a3 = { 123 };     
	Foo a4 { 123 };     
	int a5 = { 3 };     
	int a6 { 3 };     
	return 0; 
}
```

  在上例中，a3、a4 使用了新的初始化方式来初始化对象，效果如同 a1 的直接初始化。a5、a6 则是基本数据类型的列表初始化方式。可以看到，它们的形式都是统一的。这里需要注意的是，a3 虽然使用了等于号，但它仍然是列表初始化，因此，私有的拷贝构造并不会影响到它。a4 和 a6 的写法，是 C++98/03 所不具备的。在 C++11 中，可以直接在变量名后面跟上初始化列表，来进行对象的初始化。



#### **2. 成员变量默认初始化**

好处：构建一个类的对象不需要用构造函数初始化成员变量。

```c++
//程序实例
#include<iostream>
using namespace std;
class B { 
    public:
    	int m = 1234; //成员变量有一个初始值  
    	int n; }; 
int main() { 
    B b;  
    cout << b.m << endl;  
    return 0; 
}
```



#### **3. decltype  求表达式的类型**  

  decltype 是 [C++](http://c.biancheng.net/cplus/)11 新增的一个关键字，它**和 auto 的功能**一样，都用来在编译时期进行自动类型推导。

(1)为什么要有decltype

  因为 auto 并不适用于所有的自动类型推导场景，在某些特殊情况下 auto 用起来非常不方便，甚至压根无法使用，所以 decltype 关键字也被引入到 C++11 中。

  auto 和 decltype 关键字都可以自动推导出变量的类型，但它们的用法是有区别的：

```
auto varname = value; 
decltype(exp) varname = value;
```

  其中，varname 表示变量名，value 表示赋给变量的值，exp 表示一个表达式。

  **auto 根据"="右边的初始值 value 推导出变量的类型，而 decltype 根据 exp 表达式推导出变量的类型，跟"="右边的 value 没有关系**。

  另外，**auto 要求变量必须初始化，而 decltype 不要求**。这很容易理解，auto 是根据变量的初始值来推导出变量类型的，如果不初始化，变量的类型也就无法推导了。decltype 可以写成下面的形式：

```
decltype(exp) varname;
```

(2)代码示例

```c++
// decltype 用法举例 
int a = 0; 
decltype(a) b = 1;  //b 被推导成了 
int decltype(10.8) x = 5.5;  //x 被推导成了 
double decltype(x + 100) y;  //y 被推导成了 double
```



#### **4. 智能指针 shared_ptr**⭐

和 unique_ptr、weak_ptr 不同之处在于，多个 shared_ptr 智能指针可以共同使用同一块堆内存。并且，由于该类型智能指针在实现上采用的是引用计数机制，即便有一个 shared_ptr 指针放弃了堆内存的“使用权”（引用计数减 1），也不会影响其他指向同一堆内存的 shared_ptr 指针（只有引用计数为 0 时，堆内存才会被自动释放）。

```c++
#include <iostream> 
#include <memory> 
using namespace std; 
int main() {     //构建 2 个智能指针     
	std::shared_ptr<int> p1(new int(10));     
	std::shared_ptr<int> p2(p1);     //输出 p2 指向的数据     
	cout << *p2 << endl;     
	p1.reset();//引用计数减 1,p1为空指针     
	if (p1) {         
		cout << "p1 不为空" << endl;     
		}    
    else {         
    	cout << "p1 为空" << endl;     
    	}     //以上操作，并不会影响 p2     
    cout << *p2 << endl;     //判断当前和 p2 同指向的智能指针有多少个     
    cout << p2.use_count() << endl;     
    return 0; }  /*      程序运行结果：          10  p1 为空  10  1  */          
```



#### **5. 空指针nullptr**

通过将指针初始化为 nullptr，可以很好地解决 NULL 遗留的问题，比如：

```c++
#include <iostream>
using namespace std;
void isnull(void *c){
    cout << "void*c" << endl;
}
void isnull(int n){
    cout << "int n" << endl;
}
int main() {
    isnull(NULL);
    isnull(nullptr);
    return 0;
}

/*    
    程序运行结果：        
    int n
    void*c
*/          
```

#### **6. 右值引用和move语义**  

1. **右值引用**

     C++98/03 标准中就有引用，使用 "&" 表示。但此种引用方式有一个缺陷，即正常情况下只能操作 C++ 中的左值，无法对右值添加引用。举个例子：

   ```c++
   int num = 10;
   int &b = num; //正确
   int &c = 10; //错误
   ```

    如上所示，编译器允许我们为 num 左值建立一个引用，但不可以为 10 这个右值建立引用。因此，C++98/03 标准中的引用又称为左值引用。

   注意，虽然 C++98/03 标准不支持为右值建立非常量左值引用，但允许使用常量左值引用操作右值。也就是说，常量左值引用既可以操作左值，也可以操作右值，例如：

   ```c++
   int num = 10;
   const int &b = num;
   const int &c = 10;
   ```

     我们知道，右值往往是没有名称的，因此要使用它只能借助引用的方式。这就产生一个问题，实际开发中我们可能需要对右值进行修改（实现移动语义时就需要），显然左值引用的方式是行不通的。

     为此，C++11 标准新引入了另一种引用方式，称为右值引用，用 "&&" 表示。

     需要注意的，和声明左值引用一样，**右值引用也必须立即进行初始化操作，且只能使用右值进行初始化**，比如：

   ```c++
   int num = 10;
   //int && a = num;  //右值引用不能初始化为左值
   int && a = 10;
   ```

     和常量左值引用不同的是，右值引用还可以对右值进行修改。例如：

   ```c++
   int && a = 10;
   a = 100;
   cout << a << endl;
   /*    程序运行结果：        
           100    
   */          
   ```

     另外值得一提的是，C++ 语法上是支持定义常量右值引用的，例如：

   ```
   const int&& a = 10;//编译器不会报错
   ```

     但这种定义出来的右值引用并无实际用处。一方面，右值引用主要用于移动语义和完美转发，其中前者需要有修改右值的权限；其次，常量右值引用的作用就是引用一个不可修改的右值，这项工作完全可以交给常量左值引用完成。

2. **move语义**

  move 本意为 "移动"，但该函数并不能移动任何数据，它的功能很简单，**就是将某个左值强制转化为右值**。基于 move() 函数特殊的功能，其常用于实现移动语义。move() 函数的用法也很简单，其语法格式如下：

```
move( arg ) //其中，arg 表示指定的左值对象。该函数会返回 arg 对象的右值形式。
```

```c++
//程序实例
#include <iostream>
using namespace std;
class first {
public:
    first() :num(new int(0)) {
        cout << "construct!" << endl;
    }
    //移动构造函数
    first(first &&d) :num(d.num) {
        d.num = NULL;
        cout << "first move construct!" << endl;
    }
public:    //这里应该是 private，使用 public 是为了更方便说明问题
    int *num;
};

class second {
public:
    second() :fir() {}
    //用 first 类的移动构造函数初始化 fir
    second(second && sec) :fir(move(sec.fir)) {
        cout << "second move construct" << endl;
    }
public:    //这里也应该是 private，使用 public 是为了更方便说明问题
    first fir;
};
int main() {
    second oth;
    second oth2 = move(oth);
    //cout << *oth.fir.num << endl;   //程序报运行时错误
    return 0;
}

/*    
    程序运行结果：
      construct!
    first move construct!
    second move construct
*/            
```

#### 7. 正则表达式  

可以认为正则表达式实质上是一个字符串，该字符串描述了一种特定模式的字符串。常用符号的意义如下：

| 符号  | 意义                           |
| ----- | ------------------------------ |
| ^     | 匹配行的开头                   |
| $     | 匹配行的结尾                   |
| .     | 匹配任意单个字符               |
| […]   | 匹配[]中的任意一个字符         |
| (…)   | 设定分组                       |
| \     | 转义字符                       |
| \d    | 匹配数字[0-9]                  |
| \D    | \d 取反                        |
| \w    | 匹配字母[a-z]，数字，下划线    |
| \W    | \w 取反                        |
| \s    | 匹配空格                       |
| \S    | \s 取反                        |
| +     | 前面的元素重复1次或多次        |
| *     | 前面的元素重复任意次           |
| ?     | 前面的元素重复0次或1次         |
| {n}   | 前面的元素重复n次              |
| {n,}  | 前面的元素重复至少n次          |
| {n,m} | 前面的元素重复至少n次，至多m次 |
| \|    | 逻辑或正则表达式               |

### 2. C++中智能指针和指针的区别

1. 智能指针

   如果使用了new操作从堆中分配内存，则需要手动delete，c++引用了智能指针auto_ptr，但后续C++11摒弃了auto_ptr,引入了shared_ptr、unique_ptr和weak_ptr

2. 指针必须先指定其类型，再分配内存空间。

   **区别：智能指针在普通指针的基础上进行了一层封装、负责自动释放所指对象**



### 3. 智能指针有哪些，分别解决什么问题

1. C++中的智能指针有4种，分别为：**shared_ptr、unique_ptr、weak_ptr、auto_ptr**，其中auto_ptr被C++11弃用。

2. 智能指针的作用原理就是在函数结束时自动释放内存空间，避免了手动释放内存空间。

   

**（1）auto_ptr**

  auto指针存在的问题是，两个智能指针同时指向一块内存，就会两次释放同一块资源，自然报错。

**（2）unique_ptr**

  unique指针规定一个智能指针独占一块内存资源。当两个智能指针同时指向一块内存，编译报错。

  **实现原理：**将拷贝构造函数和赋值拷贝构造函数申明为private或delete。不允许拷贝构造函数和赋值操作符，但是支持移动构造函数，通过std:move把一个对象指针变成右值之后可以移动给另一个unique_ptr

**（3）shared_ptr**

  共享指针可以实现多个智能指针指向相同对象，该对象和其相关资源会在引用为0时被销毁释放。

  **实现原理：**有一个引用计数的指针类型变量，专门用于引用计数，使用拷贝构造函数和赋值拷贝构造函数时，引用计数加1，当引用计数为0时，释放资源。



**（1）auto_ptr（C++98的方案，C++11已经弃用）**

  采用所有权模式。

```c++
auto_ptr<string> p1(new string("I reigned loney as a cloud."));
auto_ptr<string> p2;
p2=p1; //auto_ptr不会报错
```

  此时不会报错，p2剥夺了p1的所有权，但是当程序运行时访问p1将会报错。所以auto_ptr的缺点是：存在潜在的内存崩溃问题。

**（2）unique_ptr（替换auto_ptr）**

  unique_ptr实现独占式拥有或严格拥有概念，保证**同一时间内只有一个智能指针可以指向该对象**。它对于避免资源泄露，例如，以new创建对象后因为发生异常而忘记调用delete时的情形特别有用。

  采用所有权模式，和上面例子一样。

```c++
auto_ptr<string> p3(new string("I reigned loney as a cloud."));
auto_ptr<string> p4;
p4=p3; //此时不会报错
```

  编译器认为P4=P3非法，避免了p3不再指向有效数据的问题。因此，unique_ptr比auto_ptr更安全。 另外unique_ptr还有更聪明的地方：当程序试图将一个 unique_ptr 赋值给另一个时，如果源 unique_ptr 是个临时右值，编译器允许这么做；如果源 unique_ptr 将存在一段时间，编译器将禁止这么做，比如：

```c++
unique_ptr<string> pu1(new string ("hello world"));
unique_ptr<string> pu2;
pu2 = pu1;                                      // #1 not allowed
unique_ptr<string> pu3;
pu3 = unique_ptr<string>(new string ("You"));   // #2 allowed
```

  其中#1留下悬挂的unique_ptr(pu1)，这可能导致危害。而#2不会留下悬挂的unique_ptr，因为它调用 unique_ptr 的构造函数，该构造函数创建的临时对象在其所有权让给 pu3 后就会被销毁。这种随情况而已的行为表明，unique_ptr 优于允许两种赋值的auto_ptr 。

  **注意：**如果确实想执行类似与#1的操作，要安全的重用这种指针，可给它赋新值。C++有一个标准库函数std::move()，让你能够将一个unique_ptr赋给另一个。例如：

```c++
unique_ptr<string> ps1, ps2;
ps1 = demo("hello");
ps2 = move(ps1);
ps1 = demo("alexia");
cout << *ps2 << *ps1 << endl;
```

**（3）shared_ptr（非常好使）**

  shared_ptr实现共享式拥有概念。**多个智能指针可以指向相同对象**，该对象和其相关资源会在“最后一个引用被销毁”时候释放。从名字share就可以看出了资源可以被多个指针共享，它使用计数机制来表明资源被几个指针共享。可以通过成员函数use_count()来查看资源的所有者个数。除了可以通过new来构造，还可以通过传入auto_ptr, unique_ptr,weak_ptr来构造。当我们调用release()时，当前指针会释放资源所有权，计数减一。当计数等于0时，资源会被释放。

  shared_ptr 是为了解决 auto_ptr 在对象所有权上的局限性(auto_ptr 是独占的), 在使用引用计数的机制上提供了可以共享所有权的智能指针。

**成员函数：**

**use_count**  返回引用计数的个数

**unique**  返回是否是独占所有权( use_count 为 1)

**swap**  交换两个 shared_ptr 对象(即交换所拥有的对象)

**reset**  放弃内部对象的所有权或拥有对象的变更, 会引起原有对象的引用计数的减少

**get**  返回内部对象(指针), 由于已经重载了()方法, 因此和直接使用对象是一样的.如 shared_ptr<int> sp(new int(1)); sp 与 sp.get()是等价的

**（4）weak_ptr**

  weak_ptr 是一种不控制对象生命周期的智能指针, 它指向一个 shared_ptr 管理的对象。进行该对象的内存管理的是那个强引用的 shared_ptr。weak_ptr只是提供了对管理对象的一个访问手段。weak_ptr 设计的目的是为配合 shared_ptr 而引入的一种智能指针来协助 shared_ptr 工作，它只可以从一个 shared_ptr 或另一个 weak_ptr 对象构造, 它的构造和析构不会引起引用记数的增加或减少。weak_ptr是用来解决shared_ptr相互引用时的死锁问题，如果说两个shared_ptr相互引用，那么这两个指针的引用计数永远不可能下降为0,资源永远不会释放。它是对对象的一种弱引用，不会增加对象的引用计数，和shared_ptr之间可以相互转化，shared_ptr可以直接赋值给它，它可以通过调用lock函数来获得shared_ptr。

```c++
class B;
class A
{
public:
    shared_ptr<B> pb_;
    ~A()
{
    cout<<"A delete\n";
}
};
class B
{
public:
    shared_ptr<A> pa_;
    ~B()
{
    cout<<"B delete\n";
}
};
void fun()
{
    shared_ptr<B> pb(new B());
    shared_ptr<A> pa(new A());
    pb->pa_ = pa;
    pa->pb_ = pb;
    cout<<pb.use_count()<<endl;
    cout<<pa.use_count()<<endl;
}
int main()
{
    fun();
    return 0;
}
```

  可以看到fun函数中pa ，pb之间互相引用，两个资源的引用计数为2，当要跳出函数时，智能指针pa，pb析构时两个资源引用计数会减一，但是两者引用计数还是为1，导致跳出函数时资源没有被释放（A B的析构函数没有被调用），如果把其中一个改为weak_ptr就可以了，我们把类A里面的shared_ptr pb_; 改为weak_ptr pb; 运行结果如下，这样的话，资源B的引用开始就只有1，当pb析构时，B的计数变为0，B得到释放，B释放的同时也会使A的计数减一，同时pa析构时使A的计数减一，那么A的计数为0，A得到释放。

  **注意**：我们不能通过weak_ptr直接访问对象的方法，比如B对象中有一个方法print(),我们不能这样访问，pa->pb*->print(); 英文pb*是一个weak_ptr，应该先把它转化为shared_ptr，如：shared_ptr p = pa->pb_.lock(); p->print();  

### 4. 简述一下 C++11 中四种类型转换

**参考回答**

  C++中四种类型转换分别为**const_cast、static_cast、dynamic_cast、reinterpret_cast**，四种转换功能分别如下：

1. const_cast

​    将const变量转为非const

1. static_cast

     最常用，可以用于各种隐式转换，比如非const转const，static_cast可以用于类向上转换，但向下转换能成功但是不安全。

2. dynamic_cast

     只能用于含有虚函数的类转换，用于类向上和向下转换

   ​      **向上转换：**指子类向基类转换。  

   ​      **向下转换：**指基类向子类转换。

   ​      这两种转换，子类包含父类，当父类转换成子类时可能出现非法内存访问的问题。

     dynamic_cast通过判断变量运行时类型和要转换的类型是否相同来判断**是否能够进行向下转换**。dynamic_cast可以做类之间上下转换，转换的时候会进行类型检查，类型相等成功转换，类型不等转换失败。运用RTTI技术，RTTI是”Runtime Type Information”的缩写，意思是运行时类型信息，它提供了运行时确定对象类型的方法。在c++层面主要体现在dynamic_cast和typeid，vs中虚函数表的-1位置存放了指向type_info的指针，对于存在虚函数的类型，dynamic_cast和typeid都会去查询type_info。

4. reinterpret_cast

​      reinterpret_cast可以做任何类型的转换，不过不对转换结果保证，容易出问题。

**注意：**为什么不用C的强制转换：C的强制转换表面上看起来功能强大什么都能转，但是转换不够明确，不能进行错误检查，容易出错。



# 操作系统

## 1. 软链接和硬链接的区别

在Linux中，链接（link）是指将一个文件名映射到一个文件的过程。在Linux中，有两种类型的链接：硬链接和软链接（也称为符号链接）。

硬链接：

1. **硬链接（Hard link）在inode上建立一个新的连接**。不同的文件可以拥有相同的inode，但硬链接不能跨越文件系统或者分区创建。
2. 硬链接不能对目录进行创建，只能对文件进行创建。
3. 当你删除原来的文件时，不会影响其他硬链接所连接的文件，因为他们都是独立的文件，除非所有的链接文件都被删除了才能真正删除这个文件。
4. 修改任何一个文件，其他的连向该文件的硬链接也会改变。

软链接：

1. **软链接（symbolic link）就是一个文件，它存放着另一个文件的路径名**。软链接是一种特殊的文件，它的内容是另一个文件的路径名，类似于Windows下的快捷方式。
2. 软链接可以跨文件系统和分区。
3. 删除原文件后，软链接无法访问原文件。
4. 修改原文件，软链接也随之改变。

总结：**硬链接是一个 inode 可以对应多个文件名，而软链接则是一个普通文件，它的数据部分存储着一个路径名，通过这个路径名间接引用到另外一个文件**。

在命令行中创建软链接可以使用`ln -s`命令，例如：

```
Copy Codeln -s /path/to/file /path/to/link
```

其中，`/path/to/file`是源文件路径，`/path/to/link`是软链接文件的路径。要创建硬链接，则省略`-s`选项即可。



## 2. 制作静态库、动态库

1. 编写代码并编译成静态库：将多个源文件编译成.o文件，然后将这些.o文件打包成.a文件，即可得到静态库。

```
$ gcc -c file1.c -o file1.o
$ gcc -c file2.c -o file2.o
$ ar rcs libmylib.a file1.o file2.o
```

2. 使用静态库：将静态库与主程序链接，生成可执行文件。

```
$ gcc main.c -o main -L. -lmylib
```



3. 编写代码并编译动态库：将多个源文件编译成.so文件

   ```
   gcc -shared -fpic file.c -o libhello.so
   ```

## 3. 什么是大端小端

**小端模式**：**低**的有效字节存储在**低的**存储器地址。小端一般为主机字节序；常用的X86结构是小端模式。很多的ARM，DSP都为小端模式。

**大端模式**：**高**的有效字节存储在**低的**存储器地址。大端为网络字节序；KEIL C51则为大端模式。

```c++
// 判断大小端
int num = 0x12345678;
char* p = (char*)&num;
if (*p == 0x78) {
    cout << "小端" << endl;
} else {
    cout << "大端" << endl;
}

```

## 4. 进程调度算法

1. **先来先服务调度算法**
2. **短作业(进程)优先调度算法**
3. **高优先级优先调度算法**
4. **时间片轮转法**
5. **多级反馈队列调度算法**

**答案解析**

1. 先来先服务调度算法：每次调度都是从后备作业（进程）队列中选择一个或多个最先进入该队列的作业（进程），将它们调入内存，为它们分配资源、创建进程，然后放入就绪队列。
2. 短作业(进程)优先调度算法：短作业优先(SJF)的调度算法是从后备队列中选择一个或若干个估计运行时间最短的作业（进程），将它们调入内存运行。
3. 高优先级优先调度算法：当把该算法用于作业调度时，系统将从后备队列中选择若干个优先权最高的作业装入内存。当用于进程调度时，该算法是把处理机分配给就绪队列中优先权最高的进程
4. 时间片轮转法：每次调度时，把CPU 分配给队首进程，并令其执行一个时间片。时间片的大小从几ms 到几百ms。当执行的时间片用完时，由一个计时器发出时钟中断请求，调度程序便据此信号来停止该进程的执行，并将它送往就绪队列的末尾；然后，再把处理机分配给就绪队列中新的队首进程，同时也让它执行一个时间片。
5. 多级反馈队列调度算法：综合前面多种调度算法。

## 5. 进程空间从高位到低位

![img](D:\WorkData\MarkdownData\StudyNotes\assets\87B82FF535E2DBDA131AF8B26A3F8BA5.png)

代码段-> 初始化数据段->未初始化数据段->堆（从低到高）->共享空间->栈（从高到低）

## 6. 操作系统如何分配和管理内存

操作系统通常通过以下方式申请和管理内存：

1. **内存分配**：当一个进程需要内存时，它会向操作系统发送一个请求。操作系统会查看可用的内存空间，然后将一块空闲的内存分配给该进程。这个过程被称为内存分配。
2. **内存映射**：操作系统还可以将磁盘上的文件映射到内存中，使得进程可以像访问内存一样访问文件。这个过程被称为内存映射。
3. **内存保护**：为了保证不同进程之间的内存不发生冲突，操作系统会为每个进程分配一段单独的地址空间。同时，操作系统也会对内存进行保护，以防止某个进程意外修改其他进程的内存数据。
4. **内存回收**：当一个进程终止时，操作系统会回收该进程所占用的内存空间，并将其标记为空闲状态，以便其他进程可以重复利用这些空间。

总体而言，操作系统通过分配、映射、保护和回收内存等手段来有效地管理内存，使得不同进程可以在共享资源的同时互相隔离，从而保证整个系统的稳定性和安全性

## 7. 使用虚拟内存的好处

**虚拟内存**：操作系统为每一个进程分配一个独立的地址空间，但是虚拟内存。虚拟内存与物理内存存在映射关系，通过页表寻址完成虚拟地址和物理地址的转换。

（1）扩大地址空间。每个进程独占一个4G空间，虽然真实物理内存没那么多。

（2）内存保护：防止不同进程对物理内存的争夺和践踏，可以对特定内存地址提供写保护，防止恶意篡改。

（3）可以实现内存共享，方便进程通信。

（4）可以避免内存碎片，虽然物理内存可能不连续，但映射到虚拟内存上可以连续。



# 进程、线程

## **1. 什么是进程，线程**

线程是CPU调度的最小单位，进程是系统资源调度的最小单位

区别：

1. 线程共享虚拟地址空间、进程不共享，即写时复制，读时共享
2. 进程创建比较耗费资源，需要复制大量进程属性信息，线程创建快，无需复制内存，也无需复制页表
3. 线程之间数据共享，只需要将数据写入共享变量中
4. 进程间相互独立，如需互相通信需要通过IPC来完成



## 2. 多进程、多线程的优缺点

两者都是提高程序并发性和响应速度的技术

多进程优点：

- **进程间相互独立，一个进程出现问题不会影响其他进程**
- 操作系统可以更好进行资源分配，避免资源竞争问题
- 多进程适合于运行需要大量CPU和内存资源的任务。

多进程缺点：

- 进程间**切换代价大**
- 进程间**通信需要通过IPC**，增加通信开销
- **创建和销毁进程开销大**

多线程优点：

- 线程之间**共享进程的资源**，避免资源竞争
- 线程切换代价小，不需要像进程一样重新分配资源
- 可以利用多核CPU，提高系统性能

多线程缺点：

- 多线程间资源共享存在**线程安全问题**，需要采用同步、锁、信号量等线程同步技术。
- 一个线程出现问题会影响整个进程的稳定性



## 3. 什么时候用进程、什么时候用线程

1. 创建和销毁频繁用线程
2. 需要大量数据传输用线程，因为线程切换速度快
3. 并行操作使用线程
4. 安全选进程、快速频繁选线程



## 4. 多进程、多线程同步的方法

**多进程：**

1. 管道 2. 信号 3. 共享内存 4.信号量 5. 消息队列 6. socket

**多线程：**

1. 信号量 2.读写锁 3.条件变量 4. 互斥锁 5.自旋锁



## 5. 进程线程的状态转换

进程和线程的状态转换如下：

进程：

1. 新建状态（New）：当一个新的进程被创建时，它处于新建状态。
2. 就绪状态（Ready）：当进程具备了运行所需的所有资源，只等待系统调度器分配 CPU 时间片时，它就处于就绪状态。
3. 运行状态（Running）：当进程被分配到 CPU 并正在执行时，它就处于运行状态。
4. 阻塞状态（Blocked）：当进程在等待某些事件（比如输入/输出操作或信号量）完成时，它就处于阻塞状态。
5. 终止状态（Terminated）：当进程执行完毕或被强制终止时，它就处于终止状态。

线程：

1. 新建状态（New）：当一个新的线程被创建时，它处于新建状态。
2. 就绪状态（Ready）：当线程具备了运行所需的所有资源，只等待系统调度器分配 CPU 时间片时，它就处于就绪状态。
3. 运行状态（Running）：当线程被分配到 CPU 并正在执行时，它就处于运行状态。
4. 阻塞状态（Blocked）：当线程在等待某些事件（比如输入/输出操作或信号量）完成时，它就处于阻塞状态。
5. 等待状态（Waiting）：当线程在等待某些条件（比如其他线程的信号）满足时，它就处于等待状态。
6. 终止状态（Terminated）：当线程执行完毕或被强制终止时，它就处于终止状态。
