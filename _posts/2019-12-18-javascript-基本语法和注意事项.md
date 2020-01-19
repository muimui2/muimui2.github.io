---
title: JavaScript初级教程——基本语法和注意事项
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
key: 2019121803
cover: null
tags: JavaScript
---

学习一门语言前要知道，养成良好的编程习惯是至关重要的，能避免一些不必要的错误。下面是学习JavaScript时的最基本的语法和习惯。在定义变量之前加上 var ，以为“；”结尾，以表示这句这行已经结束，和要习惯使用注释，能帮助别人看懂和理解你的代码，提交可读性。

## 一、在定义变量之前加上 var 

在定义变量的时候，习惯使用var 申明变量，因为var没有限制变量的数据类型。另外，使用var申明的变量，是局部变量，只能在函数内部或者文件使用，因此在不同的函数内，可以申明相同的变量名，互不影响。如果不用var申明，那变量是全局变量。
例如：
```ruby
var a;
```

## 二、以为`；`结尾，以表示这句这行已经结束。

虽然你可以不写“；”浏览器中的JavaScript引擎也会把“；”补上，但是毕竟机器也会出错，它不知道我们写的代码哪里需要断哪里是连续的。所以还是乖乖手动添加“；”比较好。



## 三、{ 代码块 }

`{ }`里面的代码表示一个集合，一个整体。里面的代码可以相互嵌套。
比如：

```ruby
<script> 
function myfun(){
if(Math.random>0.5){
console.log('随即数大于0.5')
}
else
{
console.log("随即数小于0.5")
}
var dd = new Date();
console.log(dd.getDate())
}
</script>
```


上面的代码看起来是不复杂，不过在实际应用中肯定不止这么点代码，所以会看起来一头雾水，不知道哪个代码对接哪个，变量都可能找不到。所以使用{ }书写复杂的代码时，建议把里面可以写成函数的尽量学成函数来优化代码。

例如：我可以输出时间日期的代码拿出来写成一个函数，只需要在myfun()中调用就可以了，拿出来的函数还可以在其他地方调用，是不是一举两得呢。

```ruby
<script> 

function new_date(){
var dd = new Date();
console.log(dd.getDate())
}//时间日期函数
function myfun(){
if(Math.random>0.5){
console.log('随即数大于0.5')
}
else
{
console.log("随即数小于0.5")
}
new_date();//调用函数
}
</script>
```

上面两段代码的结果都是一样的，很明显第二种的逻辑要清晰很多，在代码量多的时候更能体现。



## 四、注释：

留意到我上面的代码没，我在代码中用“//”解析了我某段代码的用处。这就是JavaScript中的单行注释。出此之外还可以用“/* */”来注释代码块。

合理的使用注释能让被人看懂你的代码，提高可读性，同时也方便自己看懂也检查。

推荐阅读：


[JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.html)

[JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)


[JavaScript变量作用域及关系简明教程](https://muitlog.com/2019/12/10/JavaScript%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F.html)


[JavaScript常见操作字符串方法](https://muitlog.com/2019/12/06/javascript%E6%93%8D%E4%BD%9C%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

[if...else, if...if...else和if...else if的使用情况](https://muitlog.com/2019/12/06/ifelse-ififelseifelse-if.html)