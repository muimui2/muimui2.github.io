---
title: if...else, if...if...else和if...else if的使用情况
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019120601
---

搞清楚if...else, if...if...else和if...else if的使用情况尤为重要，因为条件的不同执行的结果不同，甚至相反。所以本章带大家一起来区分if...else, if...if...else和if...else if的使用情况，结合例子理清楚逻辑其实也很简单。

## 情况一：if...else...

当if中的条件满足的时候，不会执行else中的语句。
```

var num=10;

if(num>2){
console.log('num>2')
}
else{
console.log('num>10')
}

// 输出num>2

```




## 情况二：if...if...else...
同样，两个if，if中的条件只要被满足就输出。


```
var num=10;

if(num>2){
console.log('num>2')
}
if(num>4){
console.log('num>4')
}
else{
console.log('num>10')
}
// 输出num>2和num>4
```



## 情况三：if...else{ if... else...}
If...else语句嵌套在else中，如果执行最外面的else，才会执行里面的if...else...语句。


```
var num=10;

if(num<0){
console.log('num<0')
}
else{
if(num>2){
console.log('num>2')
}
else{
console.log('num>10')
}
}
// 输出num>2
```



## 情况四：if...else if...else...
这种情况其实和第二种情况是一样的，只要在最后一个else前面的条件被满足任何其中一个，程序就会跳出，不再向下执行。

```
var num=10;

if(num<0){
console.log('num<0')
}
else if(num>4){
console.log('num>4')
}
else if(num>6){
console.log('num>6')
}
else{
console.log('num>10')
}
// 输出和num>4
```




推荐阅读：


[JavaScript面向对象编程及原型链理解【重点】](https://muitlog.com/2019/12/03/javascript.html)


[XMLHttpRequest对象原理和用法理解](https://muitlog.com/2019/12/02/xml-httprequest.html)


[JavaScript高阶函数常见用法大全](https://muitlog.com/2019/12/02/JavaScript%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0.html)


[ES6之Map与Set数据类型——快速查找键值](https://muitlog.com/2019/11/29/es6-map-set.html)


[ES6 块的作用域-let以及数组和字符串语法](https://muitlog.com/2019/11/28/es6-let.html)