---
title: JavaScript操作DOM元素API大全
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019111701
---

尽管操作DOM已经很完善了,现在前端框架不仅有vue ，还有JQuary，为什么还要要JavaScript来操作DOM元素呢？

其实JQuary也是JavaScript演化而来的，其实JavaScript底层也提供了简单易操作的DOM处理API。



## 一、选择符API

一听到选择符，我们首先想到的就是css里面的选择符，没错，其实是一样的，只是JS提供了三个方法，分别对选择符做出对应的操作。

### 1、querySelector()方法

querySelector()方法接收一个选择符，如果在文档中有找到这个选择符就返回第一个元素，否则就返回null。

```
var body = document.querySelector("body");
var div = document.querySelector("#div");
var my = document.querySelector(".my");
```




### 2、querySelectorAll（）方法

和querySelector（）方法一样，也是接收一个选择符，不过不一样的是返回的是一个列表，也就是一个数组。

```
var my = document.querySelectorAll(".ssdiv");
console.log(my.length) // 4
```


### 3、matchesSelector()方法

这个方法和前面两个方法一样，也是只接收一个选择符，不一样的是返回的是布尔类型，我调用元素和该元素匹配就返回true，否则返回false。用这个方法可以判断文档中存不存在某元素。不过奇怪的事我居然敲不出这个方法。而是用另外一个方法代替的webkitMatchesSelector（），而且我的文档中明明有这个类元素呀。好吧，不管他了不纠结了。

```
if(document.body.webkitMatchesSelector(".ssdiv")){
console.log("ddsa");
}
else{
console.log("x")
}
```




## 二、元素遍历

上面我们说过，Ie浏览器不可以访问文本节点，其他的浏览器都可以，导致了一系列的问题，比如说，用 childNodes 和 firstChild 等属性时的行为不一致。为了解决这个问题新定义了五个属性。

* childElementCount：返回子元素（不包括文本节点和注释）的个数。
* firstElementChild：指向第一个子元素；
* lastElementChild：指向最后一个子元素；
* previousElementSibling：指向前一个同辈元素；
* nextElementSibling：指向后一个同辈元素；





## 三、HTML5

### 1、类操作

HTML5是在HTML4上面的扩展，不单单是元素标签的增加和语义化，还新增了其他的JavaScript API。比如说与类相关的扩充，因为我们现在大多数都是用类作为选择符，所以HTML5增加了关于选择那选择符方法，getElementsByClassName()，接收一个参数，这个参数是类选择符，往回一个数组，数组的所有元素都是NodeList。这里要注意的是，接收的这个参数可以是类的组合。传入多个类时，实排名不分先后。

```
var allCurrentUsernames = document.getElementsByClassName("username current");
// 返回在页面中同时含有这两个类的元素。
```



与此同时，HTML5还新增了一个classList属性，这个属性有增加，删除，判断，操作类的方法。

add(”类“)：把阐述字符串加到列表中。如果这个值已经存在呢，就不用添加了。

* contains（）：返回的是布尔类型的值。判定列表中是否存在给定的值。
* remove（）:从列表中删除给定的字符串。
* toggle（）:这个是反作用的方法。如果已经存在给定的值就删除他。如果没有就添加。不过不知道为什么我在练习的时候。

不能用getElementsByClassName（）方法和上面的上面的处理类的方法一起使用。而是要用getElementById（）取得元素，再进行类的操作。
例如：这里要注意的是，人家类名虽然放在输出的后面，可是他是在原来的基础上添加的，而不是复制出来添加的，elediv 指针指的是元素。

```
var elediv = document.getElementById("sdiv");
console.log(elediv) // <div class="username current dsdsads" id="sdiv"></div>
elediv.classList.add("dsdsads")
```



## 2、自定义数据属性

HTML5还增加了一个新特性，就是可以给元素质定义元素属性值。前面添加data-前缀,后面跟着想要添加的属性(data-appId),属性值不分大小写。



```
var div = document.getElementById("sdiv"); // 取得该元素。
console.log(div)
var dataapp = div.dataset.appid; // 取得元素的值。
console.log(dataapp)
div.dataset.appid = 111111; // 设置元素的属性值。
console.log(div)
```


### 3、插入标记

HTML5有两个可以插入标记的属性。分别是innerHTML和outerHTML。innerHTML会说出除了付节点之内的全部内容；outerHTML会全部输出他自己。所以如果要替换DOM元素里面的内容的话。这两个方法可以选择使用。如果要全部替换，就用outerHTML属性，如果替换表现里面的内容，就用innerHTML。

```
console.log(document.getElementById("ddiv").innerHTML); // 输出子除父节点的子节点；<div class="username current" data-appId='1212' id="sdiv"></div>
console.log(document.getElementById("ddiv").outerHTML); // 输出本身
console.log(document.getElementById("ddiv").innerHTML = '<a>夜深人静</a>')
console.log(document.getElementById("ddiv").outerHTML = "<p>夏天要结束了吗</p>")
```