---
title: JavaScript中级教程——4种循环语句使用全解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019122002
cover: /assets/images/blog-images/JS/JavaScript封面.webp
---



JavaScript 循环经常用到，以下是4种JavaScript循环语句使用详解。

## 一、for条件循环

语法：
```ruby
for (语句 1; 语句 2; 语句 3)
{
    被执行的代码块
}
```

语句1是初始条件；语句2是结束条件，也就是判断条件；语句3是递增条件。
例如：
```ruby
var sum=0;
for(var i=0; i<1000; i++){
sum=sum+i;
}
console.log(sum);//499500
```
使用JavaScript 循环一下子算出来了。

除了用于计算之外，循环最常用的地方是利用索引来遍历数组。

例如：
```ruby
var arr = ['apple','banana','cat','dog','egg','foot','god'];
var i;
for(i=0; i<arr.length; i++){
console.log(arr[i]);
}

```


简单的几行代码就可以把数组里面的元素遍历一次。

既然`for()`里面的是循环条件，如果我什么条件也不添加，会怎么样呢？
如果`for( )`没添加任何条件，那应该是这样书写的`for(;;)`因为条件是空，可是还得保持3个条件的语法格式。

例如：
```ruby
for(;;){
if(i>1000){
break; 
}
sum=sum+i;
console.log(sum)
}
```
 然后就会发现，测试的浏览器卡住了，因为for(;;)会进入死循环，也就是会无线循环。浏览器都要崩溃了。这时候要在循环体里面添加break来退出循环。

## 二、for...in...遍历对象

`for...in...`用户遍历对象的属性的循环语句。可以把对象的所有属性罗列出来。
例如：
```ruby
var project = {
name:'小明',
age:18,
school:'附中',
father:'大明',
mother:'阿芳',
'best-friend':'小红',
address:'北京路',
phone:'13314756284'
}
for(var i in project){
console.log(i);
}

```


因为我们知道，对象会继承父类的属性，所以当我们想要遍历出对象属性的时候，过滤掉那些继承的属性，只得出改对象的属性，我们应该用`hasOwnProperty( )`方法。添加过滤添加就可以。

例如：
```ruby
for(var j in project){
if(project.hasOwnProperty(j)){
console.log(j)
}
}
```



上面是遍历出对象的属性，如果把`for...in...`用在数组中，得到的是数组的索引。

例如：
```ruby
var arr1 = ['apple','banana','cat','dog','egg','foot','god'];
for(var i in arr1){
console.log(i)
}

```

要注意的是，这种方式的出来的索引不是number类型的，而是字符串类型的，因为索引也是数组的属性。


我们也可以用这种索引的方式访问数组。

例如：
```ruby
var arr1 = ['apple','banana','cat','dog','egg','foot','god'];
for(var i in arr1){
console.log(arr1[i])
}
```


## 三、while条件循环

For循环有三个条件，二、而while循环只有一个条件，只要满足就继续循环，一旦不满足就结束循环，比较好理解。
例如：
```ruby
var i =0;
var sum=0;
while(i<1000){
sum=sum+i;
i+=1;
}
console.log(sum)//499500
```
当`i=999`时，进行`while`判断，小于1000，继续循环，循环体中`i +1 = 1000`，回头继续进行`while`判断，发现1000不小于1000，不满足条件，所以退出循环。

## 四、do...while循环

do...while是先执行混循环体再进行判断条件是否满足，所以无论如何，循环体都会至少执行一次。
```ruby
var i = 0;
var sum = 0;
do{
sum=sum+i;
i+=1;
}while(i<1000)
console.log(sum)//499500

```

推荐阅读：



- [JavaScript初级教程——基本语法和注意事项](https://muitlog.com/2019/12/18/javascript-基本语法和注意事项.html)
- [javascript历史以及ECMAScript理解](https://muitlog.com/2019/12/16/javascript历史.html)
- [JavaScript函数及其参数使用详解](https://muitlog.com/2019/12/12/JavaScript函数.html)
- [10道JavaScript面试题——画重点](https://muitlog.com/2019/12/12/10javascript.html)
- [JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript数据类型.html)
- [JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)



