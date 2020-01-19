---
title: JavaScript递归函数和闭包——简单易理解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019111602
---

在JavaScript程序中，比较重要的是函数的运用。这章节要介绍的是递归函数和闭包。记得以前JavaScript面试的时候，面试官问我闭包是什么，有没有经常运用，我都不大清楚闭包是什么，然后，我是经常使用的，只不过不知道这个东西就是闭包而已。


定义的函数有两种，一种是函数声明，第二种是函数表达式。关于函数声明，最重要的一个特征就是函数声明的提升，就是可以在函数声明之前调用，也不会出错。

函数表达式就是把一个匿名函数复制给一个变量，这个变量就变成了函数的名字，这个函数表达式就不能提前在函数表达式之前调用，否则会出错。


## 一、递归函数

**递归函数是在一个函数通过名字调用自身的情况下构成的。** 我们在Function的引用类型中提过，由于函数名是指指针，于函数表达式其实没太多关系，如果在函数表达式内也使用函数名，那改变函数名的时候，也造成了许多麻烦，不科学，所以我们可以使用arguments.callee指向参数的原函数，也就是正在执行的原函数的指针。
可是在严格模式下，不能通过脚本访问arguments.callee，所以，我们可以通过命名函数表达式，这种方式无论是在严格模式还是非严格模式都可以。

例如：
```

"use strict"
function factorial(num){ 
if (num <= 1){ 
return 1; 
} else { 
return num * arguments.callee(num-1); 
} 
}

// 改进
var ff = function f(num){ // 把命名函数复制给变量，从而可以把arguments.callee直接写成命名函数的名字
if (num <= 1){ 
return 1; 
} else { 
return num * f(num-1); 
} 
}
console.log(factorial(10)) // 3628800 严格模式下出错
console.log(ff(10)) // 3628800 
```





## 二、闭包

我们知道JS中没有块作用域，只有全局作用域和函数作用域，所以函数和变量之间的结合体就是闭包，这里的变量可以是全局变量中的，也可以是函数作用域中的。所以如果一个函数本身内部定义了变量，或者引用了全局作用域中的变量，那它自己就是一个闭包。
这样说是不是很容易懂了。