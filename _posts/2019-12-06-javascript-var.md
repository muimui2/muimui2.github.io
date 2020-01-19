---
title: JavaScript中var的作用详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019120602
---

JavaScript 中`var`用于定义一个变量。不过在JavaScript中定义的变量他们有几种作用域，处在什么样的局域决定了他们的变量属于什么类型的变量。有局部变量和全局变量。



## 一、局部变量

另外， 变量名之前要带 var 来申明变量，否则该变量就是全局变量。用var 申明的变量只可以在函数内部使用。

例如：
```

var i = 12;
console.log(i)//12
function myfun(){
var i = "我就是我";
console.log(i)//我就是我
}
myfun();
```




## 二、全局变量

即使是相同的变量名也不会有冲突，但是如果不用var 就是全局变量了。
例如：变量i 已经在函数中被字符串替代。

```
i = 12;
function myfun(){
i = "我就是我";
console.log(i)
}
myfun()//我就是我 
console.log(i)//我就是我 


```



## 三、严格模式

这其实是一个JavaScript 设计的缺陷来的，所以后来ECMA推出了strict模式来解决这个问题。在代码的开始部分加入字符串“`use strict`”，支持strict模式的浏览器就会在严格模式上执行JavaScript代码，强制使用var申明变量，否则就会报错，告诉程序员哪里没有出了问题。未支持strict模式的浏览器就是只是把“use strict”编译成了一句字符串，没有任何意义。不过现在大多数浏览器都支持strict模式。

例如：严格模式下的全局变量不被允许。
```
"use strict"
i = 12;
function myfun(){
i = "我就是我";
console.log(i)
}
myfun()//我就是我 
console.log(i)//我就是我 


```

## 四、变量的状态

变量可以区分未静态变量和动态变量。
动态变量是是用var 申明的变量，可以是任意类型的变量，比较灵活。在赋值过程中变量就不断根据所赋值的数据类型变化而变化。
例如：
```

var a = "hello";
console.log(typeof(a))//string
a = 1212;
console.log(typeof(a))//number
console.log(a)//1212

```

静态变量的数据类型是已经定好了的，不可变得，如果改变数据类型就会出错。
例如：不能把字符串“123”赋值给整形a。
```
int a = 12;
a = "123"
```

更多推荐阅读：

[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)