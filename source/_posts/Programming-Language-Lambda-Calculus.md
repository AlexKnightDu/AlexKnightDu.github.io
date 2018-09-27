---
title: Programming Language - Lambda Calculus
date: 2018-04-19 20:50:21
tags: [Programming Language, Note, Lesson] 
mathjax: true
---


 <center> <h2> 类型系统与Lambda演算 </h2> </center>

### 语义形式
- 操作语义通过定义一个简单的抽象机器来说明一个程序语言的行为。通过定义的语言来描述抽象机器的状态，通过转换函数来定义机器的行为，类似FA和PDA的感觉。   
在《计算的本质》里提到了大步语义和小步语义，一个是先递归算子表达式，另一个是迭代一步步规约。
- 指称语义采用更为抽象的语义：一个项的语义不仅是机器状态的序列，而且是某个数学对象，如一个数和一个函数。一个语言的指称语义是由一个语义域集合和将项映射到域中元素的解释函数所组成。   
指称语义的一个主要优势在于它对求值的细节进行抽象，突出语言的本质概念。
- 公理语义对于这些规则采用更为直接的处理方式：不是首先定义程序的行为（给出某种操作语义或指称语义），然后推导出这个定义的规则，而是公理方法用规则本身作为语言的定义。一个项的语义就是关于这个项我们能证明的东西。


--

### 无类型Lambda演算
*Pure lambda functions*  

Lambda演算语法由3种项组成：
- 变量x本身是一个项
- 一个变量x在项$t_1$中的抽象，记为$\lambda x.t_1$
- 一个项$t_1$应用于另一个项$t_2$时，记为$t_1 \ t_2$

即 $$ t ::= \\  x \\ \lambda x.t \\ t \ t $$



一个不含自由变量的项称为封闭项，封闭项也称为组合子。最简单的组合子，称为恒等函数： 
$id = \lambda x.x; $

##### 操作语义
纯形式的Lambda演算没有内置的常量或原语算子（算数运算、条件子等）。项运算的唯一含义是将函数应用到本身是函数的参数：
$$(\lambda x.t_{12})t_2 \rightarrow [x \mapsto	t_2] t_{12}$$
根据上述规则重写的一个约式的操作称为beta归约。
归约的求值策略：

- 全beta归约，任何时刻可以归约任何一个约式。
- 规范顺序策略，最左边最外面首先归约。
- 按名调用，在规范顺序基础上，不允许在抽象内部归约 （Haskell等）。
- 按值调用，最外面的约式可以归约，且只有当该约式的右边已经归约为值时才能进行归约（大部分语言）。

##### 多参数
Currying 
$$f = \lambda (x,y).s \ \Rightarrow	\ f = \lambda x. \lambda y. s $$

##### Church bool
$$tru = \lambda t. \lambda f. t$$
$$fls = \lambda t. \lambda f. f$$
$$test = \lambda l. \lambda m. \lambda n. l \ m \ n$$

##### Pair
...

##### Recursion
$$omega = (\lambda x. x\ x)(\lambda x. x\ x)$$
$$fix = \lambda f.\ (\lambda x.\ f\ (\lambda y. x\ x\ y))(\lambda x.\ f\ (\lambda y. x\ x\ y))$$
$$(g = \lambda f)\ \ then\ \ (fix\ g)$$

##### 操作语义
无类型Lambda运算 Call-by-value  
语法： 
$$ t ::= \\  x \\ \lambda x.t \\ t \ t $$
$$ v ::= \lambda x.t$$

求值：
$$\frac{t_1 \rightarrow t_1'}{t_1 \ t_2 \rightarrow t_1'\ t_2}\ (E-APP1)$$
$$\frac{t_2 \rightarrow t_2'}{v_1 \ t_2 \rightarrow v_1\ t_2'}\ (E-APP2)$$
$$(\lambda x.t_{12})\ v_2 \rightarrow [x\mapsto v_2]\ t_{12}\ (E-APPABS)$$

#### 项的无名称表示
如何决定每个项的单一表示，特别是变量的出现如何表示。   
Nicolas de Bruijin技术 —— 将变量出现直接指向它们的绑定器，而不是按名称引用它们。

--

### 类型算术表达式
$t:T$
算术表达式的类型关系是项和类型之间的最小二元关系，满足类型规则中所有规则的实例。


##### 安全性 = 进展 + 保持
- 进展：一个良类型项不会受阻，要么是一个值，要么根据求值规则做下一步
- 保持：如果一个良类型项做进一步求值，则所得到的项也是良类型的

--


### 简单类型的Lambda演算
一般地，借助于项的类型注释来检查类型的语言成为显式类型化语言，要求类型检查器自己推导或重构这个信息的语言称为隐式类型化语言。

一个类型化上下文（也称一个类型环境）$\Gamma$是一个变量和它们类型的序列，并且逗号算子(comma)通过在右边加入一个新绑定来扩展$\Gamma$。   

抽象类型规则的一般形式为：
$$\frac{\Gamma ,x:T_1 \vdash t_2:T_2}{\Gamma \vdash \lambda x:T_1.t_2:T_1 \rightarrow T_2}$$
其中前提比结论多一个假设。  
变量的类型规则可以直接得到，一个变量可以有任何我们当前假定的类型：
$$\frac{x:T \in \Gamma}{\Gamma \vdash x:T}$$
应用类型规则：
$$\frac{\Gamma \vdash t_1: T_{11} \rightarrow T_{12} \ \  \Gamma \vdash t_2 : T_{11}}{\Gamma \vdash t_1 \ t_2 : T_{12}}$$


### 扩展
#### let 绑定
$$let\ x = t_1\ in\ t_2\ \ \triangleq \ (\lambda x:T_1.t_2)\ t_1$$


#### Environment model 

--
*Reference*   
- *<< Types and Programming Languages >>*   *Benjamin C. Pierce*  
- *CS383 by Kenny Zhu*  
