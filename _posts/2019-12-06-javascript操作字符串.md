---
title: JavaScript常见操作字符串方法
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019120603
---

JavaScript 中的字符串是用‘’或者“”括起来的字符表示的。所以如果字符串中也包含了这两个符号就需要使用到装换了。本章的内容是JavaScript常见的字符串的操作方法，包含字符串的换行，拼接和查找字符串中的字符。


例如：
```
var a = 'hello world'
console.log(a)
var i = "i'm ok"
console.log(i)
var j = "i\'m \"ok\""
console.log(j)

```


## 一、字符换行问题

字符串换行可以用【\n】换行。另外ES6新增了一种字符串换行规则，免得麻烦的写【\n】，就是把字符串两边的“”或者‘’换成反引号。例如：`...`。反引号就是在键盘上方1的的左边。
```
var p = `幸福地
麻木`
console.log(p)
var e = '街都\n不够行'
console.log(e)
```



## 二、连接字符

连接字符我们可以用【+】，像数学那样把字符串相连起来。
可是ES6有了新玩法，就是把要相连的字符放在${ }里面，然后${ }也是放在反引号里面。

例如：

```
var name = 'MM';
var age = 18;
console.log("你好，"+name+"你今年"+age+"岁吗？")
console.log(`是的，我是${name},今年${age}。`)

```
 
当然不是所有浏览器都支持ES6，所以在使用反引号的时候最好还是先检测你的浏览器支不支持ES6。否则还是用回老方法【+】连接字符和换行。


## 三、操作字符
其实字符串就相当于一个数组，每个字符都是一个数组元素，要取得字符串中相对应的字符，除了可以用substr等字符串截取方法之外，也可以像Array数组那样区字符。索引号从0开始。

例如:


```
var m = "月台上你身影飘渺";
console.log(m.length);//8
console.log(m[1]);//台
console.log(m[3]);//你
```

m[ ]的方法只能获取字符而不能改变字符的，而数组是可以改变数组元素的，这点要和数组区分清楚。

例如：
```
m[0]="阳"
console.log(m)//月台上你身影飘渺
```


另外还有几种方法可以操作字符串的。
比如把字符字母的大写转成小写可以用`toLowerCase()`方法，与之相反的是把小写转大写可以用`toUpperCase()`方法。

可以用indexOf搜索出自定字符串出现的位置，同样可以用这个方法找出数组中指定元素的索引。

例如：
```
var m = "月台上你身影飘渺";
console.log(m.indexOf("你"))//3

var arr = ['月','台','上','身','影']
console.log(arr.indexOf("月"))//0


```

推荐阅读：

[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)