---
title: JavaScript变量作用域及关系简明教程
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019121002
---

在JavaScript中，变量有全局作用域和局部作用域，在全部中定义的变量在局部中能访问到，在局部中定义的变量在全局中不能访问到。

![](/assets/images/blog-images/JS/局部-全局作用域.jpg)

例如下面的例子中，在函数外部，找不到变量i，而可以引用全局变量j。

```

var j = 2;
function add(){
var i = 2;
console.log(i+j);
}
console.log(i)// ReferenceError: i is not defined
add();//4
```



## 一、提升变量

JavaScript的函数有个特点，就是函数会先扫描整个函数体，把申明的变量提到函数体的开头。形成了先定义后执行的顺序。如下的例子1中，在执行函数的时候，没报错，而是输出NaN，没报错的原因其实是在输出的时候，其实已经知道j是存在的，只是没赋值。试着把var j；提到var i=1；如例子2，跟例子1这个函数没区别。所以可以知道是JavaScript函数是会把变量提到函数体的最前面，可是不会把赋值提到前面。JavaScript看到的函数其实是例子2中的函数。
所以我们在书写函数的时候，尽可能养成好的习惯，把变量手动提到函数体的前面，免得带来不必要的麻烦。

例如1：

```
function fun(x){
var i = 1;
console.log(arguments[0]+i+j);//NaN
var j = 2;
}
fun(10);


例子2：
//把变量j提到前面。
function fun(x){
var i = 1;
var j;
console.log(arguments[0]+i+j);//NaN
}

fun(10);
```



## 二、全局作用域

无论是变量还是函数，在全局作用域中，都会被默认添加为window的属性。定义函数的时候，我们知道有两种方法，可以把一个匿名函数赋值给一个变量，所以其实这个这个变量也是window的属性。全局作用域里面的函数或者是变量都可以被全局对象window调用。
只是我们在书写的时候，把window省去了。
例如：

```
var i = 1;
var fun = function(){
alert(i)//输出：1
}

function myfun(x){
var i = 1;
var j = 2;
console.log(arguments[0]+i+j);//输出：13
}

alert(window.i);//输出全局变量中的i
window.fun();//使用全局对象window调用函数
window.myfun(10);

```



## 三、局部作用域

我们知道局部作用域里面的变量不能拿到全局作用域中使用，只限在局部作用域中使用，可是有一种情况，比如for循环中定义的变量i，i在for之外还可以被使用，如果想要定义for的局部作用域，只在for循环体中使用变量i，不给局部函数所使用，那我们需要定义块级作用域。
为了解决这个问题，ES6标准中定义了新的关键字let，使用let申明的变量具有块级作用域。
例如：

```
function fun(){
var arr =['A','B','C'];
for(var i=0; i<arr.length; i++){
console.log(arr[i])//输出A,B,C
}

console.log(i)//在for循环中定义的变量，输出3
}


function myfun(){
var sum = 0;
for(let j = 0; j<5; j++){
sum = sum + j;
}
console.log(sum);//10
// console.log(i)//会报错
}


fun();
myfun();
```


推荐阅读：

[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)