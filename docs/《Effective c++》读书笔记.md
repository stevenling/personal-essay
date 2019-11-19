## 55 个条款

### 1. 视 C++ 为一个语言联邦

把 C++ 视为多个次语言组成的联邦。

- C

- Object-Oriental C++  
    面向对象的思想

- Template C++  
    泛型编程
- STL

### 2. 尽量以 const，enum，inline 替换 #define

#define 的记号有可能没进入记号表中，用 const 代替，const 定义的常量一定会被编译器看到，则一定会进符号表中。

#define 不能用来定义 class 的成员变量，也不能提供封装性，const 成员变量是可以封装的。

形似函数的宏，最好用 inline 函数替换 #define

### 3. 尽可能使用 const
