# You-Dont-Know-js
you dont know js 读书笔记


### <a href="#作用域">一. 作用域是什么</a>  
### <a href="#词法作用域">二. 词法作用域</a>
### <a name="作用域">一. 作用域是什么</a>

#### 变量的赋值  
变量的赋值会进行两个动作，首先编译器会在当前作用域下声明一个变量（如果作用域已经存在该变量则声明无效）。然后js引擎会在该作用域查找该变量，如果找到了则给变量赋值。如果没有找到，则在上一级作用域继续查找。如果到全局作用域仍然没有找到，则会抛出异常。  

#### 遍历嵌套作用域规则  
遍历嵌套作用域链的规则很简单:引擎从当前的执行作用域开始查找变量，如果找不到， 就向上一级继续查找。当抵达最外层的全局作用域时，无论找到还是没找到，查找过程都 会停止。  

#### 异常类型  
ReferenceError 同作用域判别（在作用域中找到某变量）失败相关，而 TypeError 则代表作用域判别成功了，但是对 结果的操作是非法或不合理的。  
  
#### 作用域
作用域是一套规则，用于确定在何处以及如何查找变量(标识符)。如果查找的目的是对
变量进行赋值，那么就会使用 LHS 查询;如果目的是获取变量的值，就会使用 RHS 查询。
    
         
### <a name="词法作用域">二. 词法作用域</a>

#### 词法作用域  
词法作用域就是定义在词法阶段的作用域。换句话说，词法作用域是由你在写 代码时将变量和块作用域写在哪里来决定的，因此当词法分析器处理代码时会保持作用域 不变(大部分情况下是这样的)。无论函数在哪里被调用，也无论它如何被调用，它的词法作用域都只由函数被声明时所处 的位置决定。

#### js性能  
JavaScript 引擎会在编译阶段进行数项的性能优化。其中有些优化依赖于能够根据代码的 词法进行静态分析，并预先确定所有变量和函数的定义位置，才能在执行过程中快速找到 标识符。

#### 如何欺骗词法作用域  
avaScript 中有两个机制可以“欺骗”词法作用域:eval(..) 和 with。前者可以对一段包 含一个或多个声明的“代码”字符串进行演算，并借此来修改已经存在的词法作用域(在 运行时)。后者本质上是通过将一个对象的引用当作作用域来处理，将对象的属性当作作 用域中的标识符来处理，从而创建了一个新的词法作用域(同样是在运行时)。
这两个机制的副作用是引擎无法在编译时对作用域查找进行优化，因为引擎只能谨慎地认 为这样的优化是无效的。使用这其中任何一个机制都将导致代码运行变慢。不要使用它们。