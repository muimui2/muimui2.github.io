---
title: JavaScript高阶函数常见用法大全
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/reduce高阶函数.png"
key: 2019120201
---

在JavaScript中，我们称一个函数把另外一个函数作为参数，为高阶函数（Higher-order function）。JavaScript 中常见的高阶函数有以下几种。




## 一、map函数

map函数是JavaScript中已经定义好的函数，只需要拿来用就行。就像众多前端框架。map函数只针对数组，只对数组起作用，用到其他对象会报错，会提示说该函数没被定义。map函数作用在数组中，是分别对数组里面的元素进行遍历处理。说map是高阶函数，是因为map的参数中可以是函数。通过参数中携带的函数对数组进行自定义的处理。map函数返回的也是一个数组。

例如：
```
var arr = [1,2,3,4,5,6];
var person = {
name:12,
age:18
}
function ii(x){//map调用的函数
return x*x;
}
console.log(arr.map(ii));//[1, 4, 9, 16, 25, 36]

console.log(arr.map(String))//数组元素分别转字符串类型

var arr1 = ["1","2","3"];//定义一个字符串类型的数组
console.log(arr1.map(Number));//[1, 2, 3]
```


## 二、reduce高阶函数

reduce函数其实和map函数相似，都是针对数组张开的操作，是数组特有的方法函数。reduce（）接收两个参数，返回的结果作为第一个参数，第一个参数再继续和第二个参数进行运算。
表达式如下：

```
[x1,x2,x3,x4].reduce(f) = f(f(f(x1,x2),x3),x4);
```


可以这样理解：

![](/assets/images/blog-images/JS/reduce高阶函数.png)



结合例子，例如：

```
var arr = [1,2,3,4,5,6];//定义数组
function fun(x,y){
return x*10+y;
};
console.log(arr.reduce(fun));//123456


var arr1 = ['A','B','C'];
function low(a,b){
return a.toLowerCase()+b.toLowerCase();
}
console.log(arr1.reduce(low));//abc

```



## 三、filter函数

filter高阶函数和之前的之前提到的map高阶函数和reduce高阶函数一样，都是只针对数组的函数，用于筛选数组的元素，返回剩下的元素数组。filter函数把传入的函数依次作用于Array的元素，根据返回的值return ture或者是return false是否保留还是舍弃该元素。默认情况下是return false，就是筛选掉满足条件的元素，返回剩下的元素。
另外，filter函数接收多个参数，通常第一个参数标示数组元素，第二个参数标示数组索引，第三个参数标示数组本身。
例如：

```
var b = [1,2,3,4,5,6,7,8];
var c = b.filter(function(x){
return x%2!==0;

})
console.log(c);//[1, 3, 5, 7]


var arr3 = ['A','B','C'];
var a = arr3.filter(function(element,index,self){//filter接受的回调函数，第一个参数指向元素，第二个参数指向索引，第三个参数指向数组本身
console.log(element);//数组元素
console.log(index);//索引
console.log(self);//输出数组自身
// return false;//筛选掉上面的元素后返回空数组
return true;//保留元素，返回数组
});
console.log(a)// ["A", "B", "C"]

```



## 四、sort函数

### 1、ASCII编码标准

sort高阶函数是自定义对数Array进行排序。那是依据什么排序的呢？大小？我们知道Array数组元素可以是字符串，那字符串之间怎么比较大小排序？
我们来看看下面的例子：

```
var arr = ['null','String','number','undefined','Object'];
console.log(arr.sort());//["Object", "String", "null", "number", "undefined"]
var arr1 = [11,8,32,22];
console.log(arr1.sort());//[11, 22, 32, 8]
```

你是否蒙了？不知所措？sort（）到底是根据什么排序的？其实sort（）函数是根据ASCII编码排序的？什么是ASCII编码？ASCII编码是把数字、字母（包含字母大小写）和其他符号（例如：例如*、#、@等），所有的数据在进行运算时都要转换成二进制数来表示的标准。所以上面的例子中，无论是比较字符串还是比较数字，都会先转换成二进制再进行比较。
那问题来了，我怎么知道ASCII编码的规则？我们大概记住常用的可以了，其他的可以查询。
大小规则：
数字之间比较0-9从小到大
字母之间比较，小写字母大于大写字母，后面的字母大于前面的字母
了解到到以上的ASCII编码标准，我们就能轻松的比较数组和字母的数组。


### 2、自定义排序

上面的默认排序的都是从小到大，如果我们要倒序那该怎么办？sort（）函数是可以高阶函数，可以接受一个函数作为参数进行自定义排序。
例如：

```
var arr3 = [11,8,32,22];
var result = arr3.sort(function(x,y){
if(x>y){
return -1;
}
if(y>x){
return 1;
}
else{
return 0;
}
});
console.log(result);//[32, 22, 11, 8]
```

函数中返回的1或者-1是控制数组排序的方式。在实际操作中，返回1还是-1条件而定。


## 五、array函数

除了以上几个非常实用的高阶函数之外，Array对象还给我们提供了以下几个非常简单实用的高阶函数，保证你你看就会了。

### 1、every（）函数

every（）函数用于遍历数组内的所有元素是否符合条件。这个条件是every函数所接受的参数函数。返回时结果是一个boolean值。
例如：
```
var arr4 = ['null','String','number','undefined','Object'];
var result1 = arr4.every(function(x){
return x.length>5;
});

console.log(result1);//false 因为不是所有元素的长度都大于5

```


### 2.、find（）函数

find（）函数根据所接收的函数作为条件，根据这个条件，查找数组满足条件的第一个元素，如果找到了就返回这个元素，否则就返回undefined。
例如：

```
var arr5 = ['A','a','b','B'];
var result2 = arr5.find(function(x){
return x.indexOf('A') == 0;
});
console.log(result2);//返回'A', find（）返回的是满足条件数组的元素
```


### 3、findIndex（）函数

上面已经学习过了find（）函数，放回的是元素。那么可以猜想findIndex（）函数返回的是满足条件的索引值。
```
var arr5 = ['A','a','b','B'];
var result2 = arr5.findIndex(function(x){
return x.indexOf('A') == 0;
});
console.log(result2);//返回0, findIndex（）返回的是满足条件的数组的元素的索引值
```


### 4、forEach（）函数

forEach（）函数其实和map相似，都是遍历数组内的元素，分别把元素作为参数传入函数参数中。不同的是map返回的是一个新的数组，而forEach只是遍历元素输出。
例如：
```
var arr6 = ['d','a','b','c'];
arr6.forEach(function(x){
var result3 = x.toLocaleUpperCase();
console.log(result3);//分别输出'D','A','B','C'
})
```

以上介绍了JavaScript数组中的高阶函数的用法。
推荐阅读：

[vue element-UI实现分页查询](https://muitlog.com/2019/12/01/vue-element-ui.html)


[vue之Mixins混入结合图例易理解](https://muitlog.com/2019/11/29/vue-mixins.html)


[前端引入模板的4种方法](https://muitlog.com/2019/11/27/%E5%89%8D%E7%AB%AF%E5%BC%95%E5%85%A5%E6%A8%A1%E6%9D%BF%E7%9A%844%E7%A7%8D%E6%96%B9%E6%B3%95.html)


[vue之计算属性和监听属性——快速入门](https://muitlog.com/2019/11/27/vue%E4%B9%8B%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E5%92%8C%E7%9B%91%E5%90%AC%E5%B1%9E%E6%80%A7.html)


[vue如何创建路由vue-router](https://muitlog.com/2019/11/27/vuevue-router.html)