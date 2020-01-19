---
title: JavaScript对象方法及this用法详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019121001
---

函数也有作用域，在一个函数内定义一个函数，那里面的函数并不会自己调用，也是要调用该函数才行。函数也有作用域。

例如：
```
function add(){
var i = 1;
console.log(i);//输出：1
var myfun = function(){
console.log('函数B');//输出：函数B
}
myfun();//调用最外层函数的时候，才会调用到内部函数
}

add();//调用最外层函数
```

以上是在函数内部定义的一个函数方法，如果在对象中定义函数方法被称为对象方法。那么在对象中，怎么定义函数方法呢，由该怎么调用呢？


## 一、定义函数方法

在对象中，我们可以把函数名作为对象的属性，调用方法就等于访问对象的属性那样，如下面的例子。可是为什么要写成age（），而不是age呢？因为后面跟括号（）才是对象方法，否则就是一个简单的对象属性。
例如：
```

var person = {
name:'mm',
birth:2010,
age: function () {//定义对象方法
var y = new Date().getFullYear();
return y - this.birth;
}
}

console.log(person.name)//访问属性name，输出：mm
console.log(person.age());//访问对象方法，执行函数age，输出：9
console.log(person.age)//访问到age属性，不过age不是方法，所以打印出来整个函数

```



## 二、函数this用法

也许大家也注意到了上述例子中对象方法内的this，this这个关键字在JavaScript中表示的是什么？在这个例子中又表示着什么？在JavaScript中，this关键字只指向当前对象的父对象。所以在上述例子中，this关键字指向的是person对象而不是age属性。所以单独使用this的时候，指向的是全局对象window。很多人说这个是JavaScript设计的坑，或者说是设计的缺陷，其实我并不认为是坑，因为this会随着环境的改变而改变，而不变的是它始终指向当前环境的父级对象。搞清楚这一点就可以灵活运用this关键字了，这一关键字是经常出现而且很好用的呢。
例如：

```

function getAge(){
var y = new Date().getFullYear();
return y - this.birth;
}

var person = {
name:'mm',
birth:2010,
age:getAge
}

console.log(person.age())//9
console.log(getAge())//NaN,因为this指向的是全局对象window

```

## 三、apply方法

除了可以像上面那样使用属性的方法调用一个对象外部的函数作为方法之外，还有一种方法，这是函数本身的apply方法。使用方法是带参的形式，第一个参数是需要绑定的对象，第二个参数是函数本身的参数，以数组的形式出现。
语法如下，理解为A对象应用B对象的方法。
B.apply(A, arguments)

例如：

```
function getAge(){
var y = new Date().getFullYear();
return y - this.birth;
}

var person = {
name:'mm',
birth:2010,
age:getAge
}

console.log(getAge.apply(person,[]))//输出9，理解为person对象应用getAge的方法
```

除此之外，还有一个类似于apply的方法，就是call( )，调用一个对象的一个方法，用另一个对象替换当前对象。
语法：

```
B.call(A, args1,args2);
```

不同之处是apply（）是把参数以数组的形式放在第二个参数上，而call（）是一个个按顺序传入，不是数组的形式。


推荐阅读：
[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)