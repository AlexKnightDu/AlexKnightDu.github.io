---
title: 《Effective C++》Note
date: 2018-10-27 16:02:00
tags: [Programming_language, Coding]
---

#### Item 1
C++ is big

#### Item 20
const &    
相对于直接传值带来效率的提高  
避免多余的构造和析构  
避免slicing（对象分割），派生类不会由基类复制构造产生，故也保留了本身的性质  
对于内置类型以及STL迭代器和函数对象时，习惯上都被设计为传值

#### Item 21
return object;  
stack / heap 避免调用构造函数

```C++
inline const Rational operator * (..)
{
	return Rational(..); // Just return a new object
}
```


#### Item 3 
const   
常量 参数 返回值 成员函数  
bitwise constness / logical constness (mutable)  
casting away constness 

```C++
	non_const{
		const_cast<>(const())
	}
```

#### Item 2
const, enum, inline > #define  
class专属常量 

```C++
class x{
	static const int NumTurns; // Declaration
} 
const int x::NumTurns = 1; // Definition
```
enum hack  
宏函数 --> template inline

```C++
template<typename T>
inline void callWithMax(const T& s, const T& b) 
{
	f(a > b ? a : b);
}
```


   
#### Item 7
多态基类 virtual ~()   
避免基类的析构无法把派生类的一些内容清除  
vptr

#### Item 24

#### Item 34
接口继承 和 实现继承

#### Item 4 
Initialization    
成员初值列  
non-local static 单例模式

#### Item 5 & Item 6
```C++
class Empty{
public:
	Empty() {...}
	Empty(const Empty& rhs) {...}
	~Empty() {...}
	
	Empty& operator=(const Empty& rhs) {...}
}
```
在没有reference以及const等条件限制下，编译器会自动生成这些函数，但是如果不想这些生成，则应该通过private或单独设计一个base class等方式不去定义

```C++
class Uncopyable{
protected:
	Uncopyable() {}
	~Uncopyable() {}
private:
	Uncopyable(const Uncopyable&);
	Uncopyable& operator=(const Uncopyable&);
};
```

#### Item 8
不要让析构函数抛出异常




## The C++ Programming Language
- 函数对象
- 灵巧指针
- 显式构造函数