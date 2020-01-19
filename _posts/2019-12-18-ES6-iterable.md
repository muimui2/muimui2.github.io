---
title: ES6中的iterable类型for...of和foreach遍历多维数组
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: ES6
key: 2019121801
cover: /assets/images/blog-images/JS/for-in理解图.png
---

因为Map和Set是ES6新添加的数据类型，Map可以是二维数组，所以要遍历像这种特殊的数组，ES6标准又定义了新的iterable类型，把Array，Map和Set都归纳为iterable类型。


## 一、for...of...

看到for...of...是否会想起for...in...，那我们再来复习一下for...in...的用法，例如：

```ruby
var arr = ['A', 'B', 'C'];

for (var i in arr){

console.log(i);//输出0，1，2
onsole.log(typeof(i))//string
}
var person={
name:'mm',
age:18
};
for (var i in person){
console.log(i);//输出：name,age
}
```


数组也属于对象，所以使用for...in...遍历对象得出的只是对象的key值，也就是对象的属性名，并且都是string类型的。就像是超市，for...in...遍历只是找到了货架，并不在意里面装的是啥。

![img]( /assets/images/blog-images/JS/for-in理解图.png) 

 

想要遍历到对象的值，找到货架上的商品，iterable类型集合可以通过for...of...来遍历。
例如：

```ruby
var arr = ['A', 'B', 'C'];

for (var i of arr){

console.log(i);//输出：A,B,C

}
```


用这个方法可以马上输出对象的值。所以可以猜想，for...of...循环遍历的是集合本身的元素？


![img](/assets/images/blog-images/JS/for-of理解图.png) 


我们在来多几个例子，在Map和Set中是如何使用for...of...来得到对象本身的元素的。

```ruby

var s = new Set([1,2,3,4,'mm']);

for (var x of s) { 

console.log(x);//输出：1,2,3,4,mm

}

 

var m = new Map([[21, 'x'], [32, 'y'], [53, 'z']]);

for (var x of m) {

console.log(x[0]+','+x[1]);//21,x 32,y 53,z

console.log(x)//(2) [21, "x"] (2) [32, "y"] (2) [53, "z"]

 

}

 
```


以上的例子中，使用for...of...循环遍历Set很好理解，因为Set只有key，没有value，所以输出得到的直接是对象本身的元素。而Map是一个二维数组，所以如果直接console.log(x)的话得到的是一个个数组元素，所以如果要遍历到元素数组中的，还要运用多维数组的访问元素的方法。

 


## 二、forEach( )方法

需要达到相同效果的还可以运用`forEach( )`方法，`forEach( )`是ES6标准定义的，虽然大多数浏览器都已经支持ES6，但是为了避免你能顺利的学习，所以在使用之前还是要测试一下你的浏览器是否支持。

语法：
```ruby
array.forEach(function(currentValue, index, arr), thisValue)
```

`forEach( )`方法用于调用数组的每个元素，并且将元素返回给回调函数。

**currentValue**是数组的值表示当前元素；

**index**是元素的索引；

**arr**是当前元素的数组对象。


以下是我用forEach( )方法在iterable集合中使用的方法和结果。在浏览器的控制台中我们可以看到运行的效果，在Map类型中使用的时候，可以知道这三个函数参数所表示的是什么：第一个参数标示的是数组的value值，第二个参数，标示的是元素的key值，而在一Array数组中，第二个参数标示的是索引，这点要区分开。第三个指向的是对象本身。


```ruby

var mm = new Map([['class1',60],['class2',45],['class3',55],['class4',60]])

mm.forEach(function(value,index,arr){

console.log(value)//60,45,55,60

console.log(index)//calss1,calss2,calss3,calss4

console.log(arr);//['class1',60],['class2',45],['class3',55],['class4',60]]

})

 

console.log('==========================')

var ss = new Set([1,4,3,5]);

ss.forEach(function(value,index,arr){

console.log(value)//1,4,3,5

console.log(index)//1,4,3,5

console.log(arr);//Set(4) {1, 4, 3, 5}

})

 

console.log('==========================')

var arr1 = ['A', 'B', 'C'];

arr1.forEach(function(value,index,arr){

console.log(value)//A,B,C

console.log(index)//0,1,2

console.log(arr);//(3) ["A", "B", "C"]

})
```


因为forEach( )方法中函数的三个参数不是都是必要的，所以在使用的使用视为情况和需要而定，比如在Set类型中，因为Set没有索引，所以前两个参数返回的都是元素本身。

推荐阅读：
推荐阅读：

[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)


[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)

 

 

 

 

 

 

 

 

 

 

 

 

 

 