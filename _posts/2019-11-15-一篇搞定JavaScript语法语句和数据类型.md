---
title: 一篇搞定JavaScript语法、语句和数据类型
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019111503
---

本章我们来学习JavaScript的语法，语句和数据类型。



## 一、语法


在JS中区分大小写，比如`changeColor（）`和`changecolor（）`是两个不同的函数。以【； 】号结尾为一个语句，虽然说分号可以省略，但是省略有时候会带来不必要的麻烦，所以还是每写完一句就手动加上分号比较标准。另外就是符号之间比如【=】和【+】两边最好都加上一个空格，虽然不加也不会出错，但是养成良好的书写喜欢对一个程序员来说尤为重要。{ }为一个代码块。

```
例如：
function sayhi(){
console.log(arguments[0] + "," + arguments[1]);
}
// 可以用arguments对象来获得参数
```




## 二、数据类型

JS中有6中数据类型，分别是Undefined，Null，Boolean，Number，String，Object；这6种数据类型都可以用typeof来检测出。

这里主要要说的是：
Undefined表示申明之后并没有赋值。

Null表示一个空的指针，其实就是空值，使用typeof操作符检测会返回Object，所以其实Null是一个Object类型的。有些人说其实这个是JS设计的漏洞，Undefined其实就是Null，在这里我是表示认同的，因为Undefined没找到值，也就是该值为空，而Null也是是该值为空，难道不是一样的意思？

```
console.log(typeof(null)) // object 是一个空的对象
var a;
console.log(a); // undefined 声明变量并没初始化，所以是undefined
console.log(b); // 出错 没有声明变量
console.log(typeof a); // 输出的类型是undefined
console.log(typeof b); // 即使没有声明变量，输出的类型是undefined，即使和已经声明的变量有本质的区别，但是无论那种变量都不能进行实际的操作。
var c;
var d = null;
console.log(typeof c); // undefined
console.log(typeof d); // object
console.log(typeof d == typeof c); // false undefined 值是派生自 null 值的，所以在以前的版本两个是想等的，返回true,但是因为他们的确实是不同的数据类型，所以现在现在的版本中他们是不想等的。
```




## 三、操作符

在JavaScript中，加减乘数【+，-，* 】等成为操作符，比如有一元操作符，就是只能操作一个数的操作符就是一元操作符。使用操作符可以处理在JS中的逻辑问题和数值关系，除此之外，重要的操作符还有:

```
var i = 2;
++i;
console.log(i) // 3 ++i就是自身加1，--I同理
console.log(!true) // false 布尔操作符（！）逻辑非
console.log(5 * 6) // 乘性操作符
console.log(5 + 6) // 加性操作符
if(3 < 5){ // 关系操作符
console.log(5)
}
console.log(5 == "5") //true 相等操作符（转换后相等，不包括类型）
console.log(5 === "5") // false 绝对相等（包括类型）
console.log( 5 > 3 ? 5 : 3) // 5 条件操作符 
var j = 2;
console.log(j) // 赋值操作符【=】，除此之外还有【%=】去模操作符
var n = 3,
m = 5,
p = 10; // 分别表示 var n = 3, var m = 5, var p = 10使用逗号操作符能简化重复使用var
```





## 四、语句

其实JS的语句能够体检出JS的语法特点。在JS中规定的语句称为流控制语句，它有特定的语法用法和功能，语句通常使用一或多个关键字来完成给定任务。语句可以很简单，例如通知函数退出；也可以比较复杂，例如指定重复执行某个命令的次数。
比如我们熟悉的if语句，如何满足条件继续执行，否则停止输出。还有各种循环语句，比如for,while,do...while,for...in等等；在这里就不一一列举了，都是我们在编程的时候比较常用到的具有一定规则的语句。





## 五、函数

对于任何一门编程语言，函数都是核心，函数可以封装任意多条语句，在任何地方调用，大大的提高了代码执行能力和代码的整体性。这里要说的是，我们平时经常见到的带参函数，其实是可以不写参数也是可以的，写上参数只是为了标识而已，其实你传多少个参数进去对这个函数并没影响。因为都是传到了一个对象哪里去了，函数只是从那么对象那里读取传进来的参数而已。这个对象就是arguments，这个对象就像一个数组那样记录排列着传进来的参数。
例如：

```
function sayHi(){
console.log(arguments[0] + "," + arguments[1]);
}
// 可以用arguments对象来获得参数
sayHi("Luara","15") // Luara,15

另外，如果出现相同的函数名称，在JS里面，不是定义了两次，并不具有两个函数的功能，而是会被最后一个定义的替代。例如：
function sayHi(){
console.log(arguments[0] + "," + arguments[1]);
}
function sayHi(){
console.log("12121") // 10100
}
// 可以用arguments对象来获得参数
sayHi("Luara","15") // 10100
```