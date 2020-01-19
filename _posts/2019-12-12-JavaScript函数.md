---
title: JavaScript函数及其参数使用详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019121203
---

JavaScript中经常用到函数，在函数{ }内封装了一个方法。函数具有完整性。函数有匿名函数和具名函数。

## 一、函数的定义和调用

有两种定义函数的方式。

### 【1】直接定义

定义函数用function关键字开头，后跟函数名，函数名后面的（）里面加的是参数，参数是可选的，如果带有参数则这个函数为“带参函数”，这个参数其实充当着函数的变量。{ }里面是该函数需要执行的函数体，可以有多条语句，也可以一条也没有。
例如：
```
function myfun(x){
var num = Math.random();
if(x>num){
console.log(x);
}
else{
console.log(num);
}
}
```


### 【2】函数赋值

第二种方式是匿名函数的方式，就是函数没有函数名，和以上的书写方式一样，就是没有函数名，因此可以通过赋值的方式把这个函数复制给一个变量。
例如：

```
var myfun = function(x){
var num = Math.random();
if(x>num){
console.log(x);
}
else{
console.log(num);
}
};
```


### 【3】调用函数

函数的调用比较简单，就是在需要执行该函数的地方调用调用其函数名，需要添加参数的时候加入参数。要注意的是，在传入参数的时候，我们可以任意传参，即使定义的时候并没有定义那么多参数。或者没有传入参数，只要调用，函数也会照样执行，只是会跳过包含参数的部分。
例如：
```
var myfun = function(x){//定义一个参数
var num = Math.random();
if(x>num){
return console.log(x);
}
else{
return console.log(num);
}
};

myfun(0.5, 1.2,5);//传入多个参数，后面的参数不会影响前面的参数

myfun();//跳过if（）条件，输出任意多随机数

```





## 二、函数中的return

return 语句会终止函数的执行并返回函数的值。所以当我们在函数中使用return的时候，要注意return语句的换行问题。如果把需要返回的值放在return的下一行，那这个返回值不会被执行，因为遇到return就已经终止执行函数了。这是为什么我之前提到说虽然JavaScript 引擎会帮助我们自动添加结尾的分号“； ”，但是我们还是最好就自添加。
如上面例子：
```

var myfun = function(x){
var num = Math.random();
if(x>num){
// return console.log(x);
return
console.log(x);//错误，return没分号，js引擎会自动添加分号‘；’，所以终止了函数
}
else{
return console.log(num+'.....');
}
};

myfun(0.5);
```



## 三、arguments

arguments只在函数内部起作用，是JavaScript 的一个关键字。arguments始终指向调用函数的时候传入的参数，类似于一个Array数组，可是并不是数组。利用这一关键字，我们可以知道调用函数传入的参数是什么，甚至操作参数。
例如：
```
function myfun(){
for(var i = 0; i<arguments.length; i++){
console.log(arguments[i])//输出：10,20,30
}
if(arguments[1]>arguments[0]){
arguments[0]=arguments[1];
console.log(arguments[0])//输出：20
}
}
myfun(10,20,30);

```



## 四、函数中的rest参数

我们知道，在调用函数的时候，我们可以传入任意多个参数，即使定义函数的时候并没有定义那么多个。arguments关键字是收集全部参数，那么怎么把除了函数定义的参数之外，多余的参数收集起来？
SE6标准新定义了rest参数解决这一问题，函数中的rest参数其实是一个数组，这个rest参数放在函数参数里，用于收集了调用函数时传入的其余的所有参数。
书写方式是rest参数总放在参数最后面，前面有三个点“...”用于标识这个参数的特殊用法。
例如：
```

function myfun(x,y,...rest){
if(x>y){
console.log(x+'>'+y);
}
else{
console.log(x+'<'+y);
}
console.log(rest);
}
myfun(10,20,25,45);//输出：10<20 [25, 45]
```

试了以下，如果没有传入多余的参数，会不会输出数组，答案是会的，会输出一个空数组，所以rest参数就是在函数定义的时候定义了一个空数组。

推荐阅读：

[JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.html)

[JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)


[JavaScript变量作用域及关系简明教程](https://muitlog.com/2019/12/10/JavaScript%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F.html)


[JavaScript常见操作字符串方法](https://muitlog.com/2019/12/06/javascript%E6%93%8D%E4%BD%9C%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

[if...else, if...if...else和if...else if的使用情况](https://muitlog.com/2019/12/06/ifelse-ififelseifelse-if.html)