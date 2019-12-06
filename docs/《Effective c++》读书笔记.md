## 55 个条款

### 01. 视 C++ 为一个语言联邦

把 C++ 视为多个次语言组成的联邦。

- C

- Object-Oriental C++  
   面向对象的思想

- Template C++  
   泛型编程
- STL

### 02. 尽量以 const，enum，inline 替换 #define

#define 的记号有可能没进入记号表中，用 const 代替，const 定义的常量一定会被编译器看到，则一定会进符号表中。

#define 不能用来定义 class 的成员变量，也不能提供封装性，const 成员变量是可以封装的。

形似函数的宏，最好用 inline 函数替换 #define

### 03. 尽可能使用 const

只要某值保持不变是事实，就应该说出来，编译器就会强制实施这个约束。

#### const 与 STL 迭代器

- 声明迭代器为 const

  ```cpp
  int main()
  {
      std::vector<int> vec;
      const std::vector<int>::iterator iter = vec.begin();
      *iter = 10; // 可以，改变 iter 所指向的对象
      ++iter;     // 错误，这个迭代器本身是 const，不可以改变
      return 0;
  }
  ```

  这个迭代器不得指向不同的东西，但它所指的东西的值是可以改变的。

- 声明迭代器所指的东西的值是 const

  ```cpp
  int main()
  {
      std::vector<int> vec;
      std::vector<int>::const_iterator iter = vec.begin();
      *iter = 10; // 错误，*iter 是 const，不可以修改
      ++iter;     // 可以，移动 iter
      return 0;
  }
  ```

#### const 修饰函数返回值

可以使函数的返回值一定是一个右值，这样可以降低客户错误所造成的意外，又不至于放弃安全性和高效性。

#### const 修饰成员函数

### 04. 确定对象被使用前已先被初始化

读取未初始化的值会导致不明确的行为，最佳处理办法是：**永远在使用对象之前将其初始化**。

- 内置类型，手动初始化
  > int x = 0;
- 非内置类型，在构造函数中进行初始化，规则：**确保每一个构造函数都将对象的每一个成员初始化。**

#### 构造函数初始化

构造函数的初始化有两种方式，如下：

```cpp
class CExample {
public:
    // 1. 构造函数初始化列表
    CExample(): a(0),b(8.8)
    {
    }

    // 2. 构造函数内部赋值
    CExample()
    {
        a = 0;
        b = 8.8;
    }
private:
    int a;
    float b;
};
```

最好使用成员初始化列表的方式，而不要在构造函数的函数体中使用赋值操作。**初始化列表列出的成员变量，它的排列顺序应该和它们在类中声明的顺序相同。**
