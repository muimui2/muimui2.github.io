---
title: 区分JavaScript中的基本类型和引用类型
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript基本类型和引用类型.webp"
key: 2019111501
---

本章学习JavaScript中的基本类型和引用类型以及两者的区分。
解析JavaScript中的垃圾收集机制。


![](/assets/images/blog-images/JS/JavaScript基本类型和引用类型.webp)



## 一、基本类型和引用类型的值

什么是基本类型什么引用类型？我们知道JS的数据类型有6种，而基本类型值就是**Undefined、Null、Boolean、Number 和 String**。而引用类型值指的就是**对象**。可以理解为基本类型的值就是简单的字符串和数值，这个值是放在栈中；而引用类型的值是一个对象的或者是对象的属性，这个值是放在堆中。

所以接下来就很好理解了，当赋值一个基本类型的值时，实际是把值复制到了新的变量对象上了，内存实实在在的增加了。而引用类型的值得复制只是复制了指向值得指针，并不像基本类型那样复制值，所以内存是没有增加的。
另外可以使用关键字【instranceof】来检测变量对象的类型，这里的类型指的是引用类型还是基本类型。
下图可以帮助理解：


实例：

```
var i = 5;
var j = i; // 新建一个j变量对象，并把i的值复制给j
console.log(j) // 5 
var obj = new Object(); // 创建变量对象
var obj2 = obj; // 和obj的变量对象的值相等
obj.name = 'Luara'; // 设置obj对象的值的属性
console.log(obj2.name) // Luara 结果发现obj2的值也具有这个属性，所以复制的只是指针，而不是值

console.log(j instanceof Object); // flase
console.log(obj2 instanceof Object); // true

```





# 二、执行环境及作用域

执行环境在JS中有着及其重要的地位，每个函数和对象都有它自己的执行环境，超出这个环境就不能再被使用或者访问到。一个变量只在一个执行环境中起作用，这个环境称为作用域。执行环境和作用域其实要结合起来看，例如下面的例子，变量color是全局作用域中，执行环境是window，但是在函数changeColor（）中color是全局对象中的color，所以最后输出的结果是【red】，这个其实是JS中的作用域链，在函数内部没找到color，就会往上一级寻找color变量。同理，就算相互镶嵌多几个函数作用域也是一样的用法。

例如：

```
var color = 'blue';
function changeColor(){
if(color === 'blue'){
color = 'red'; // 去上一级（全局中）查找color，所以改变的是全局中color的值
}
else{
color = 'blue'
}
}
changeColor();
console.log(color); // red 

```



另外，要特别说明一点就是**JS是没有块级作用域**的，我们知道用`{ }`起来的代码块具有整体性，比如一个函数，在函数里面的变量具有局部作用域，但是如果一个`if`或者是一个`for`也是用`{ }`起来，那里面的变量是否具有布局作用域？答案是否定的，在全局作用域中也能访问到。如下是个典型的例子，其实setTimeout是在外部访问变量i。

例如：
```

for(var i = 0; i < 5; i++){
setTimeout(function(){
console.log(i) // 5次输出5
},0)
}
// 这是个典型的例子，其中包含了定时器，把定时器放在for里面，执行了5次
// 把上面的例子写成：
for(var i = 0; i < 5; i++){
}
setTimeout(function(){
console.log(i) // 5
},0)

```



## 三、垃圾收集

关于JavaScript中的垃圾收集，其实我们不必要担心，只要我们不要定义太多的变量在全局作用域中就好，因为定义在函数中的变量，一旦函数执行完毕，也会自动释放变量腾出内存空间来。如果实在没办法，要手动清理，我们可以在使用完变量之后手动设置‘null’值就可以了。关于JS的垃圾收集机制，一般是在浏览器上完成，所以每个浏览器会不同。