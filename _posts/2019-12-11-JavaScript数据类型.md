---
title: JavaScript数据类型——前端入门
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019121101
---

JavaScript的数据类型就只有6种，很好记。

## 一、Number

```
console.log(typeof(12))
console.log(typeof(NaN))//not a number 无法计算结果
console.log(typeof(Infinity))//无穷
```

Number类型就是我们平时看到的数字，负数和小数点也属于number类型。NaN和Infinity比较特殊，NaN不属于一个数字，但它其实是数字类型，只不过这个结果不是一个数字，没有人知道是什么，甚至连NaN自己也不知道。

所以：

```
if(NaN==NaN){
console.log('我我等于我自己')
}
else{
console.log('我不知道我自己是谁')
} //结果输出：我不知道我自己是谁


另外Infinity：
if(Infinity<999999999){
Console.log("Infinity不是无穷数")
}
else{
console.log('Infinity是无穷数')
}//输出结果：Infinity是无穷数

```

## 二、string
字符串是用‘’或者是“”括起来的任意值。我们已经在JavaScript对字符串的操作和js查找字符位置中介绍过。
例如：
```
console.log(typeof('123'))//结果输出string

```


## 三、boolean

布尔值只有两个值，true  or  false用于判断结果的真假。
```
console.log(typeof(true==true))//boolean

console.log(typeof(2>3))//boolean

```


## 四、null

Null表示一个空的值，既不知0，也不是‘’，表示什么也没有。


## 五、undefined
Undefined表示未定义。就是找不到这个数或者变量从哪里来，没有根据。
```
console.log(typeof(a))//undefined
```


## 六、对象
 对象其实就是一个大的变量，包含的信息比较多的一个集合。比如数组就是一个对象。
```
var a = [1,2,3,4,5,6,7,8,9]
console.log(typeof(a))//object
```

再例如：一组由键-值组成的无序集合

```
var person = {
name : "Luara",
age:18,
add:'北京市三环内',

};

console.log(typeof(person))//object
```


null和undefined，非常相似，有些程序员甚至把他们看做是一个东西，其实是不同的，null表示没有对象，没有值，一个也没有；而undefined则表示此处应该有一个值，而该值还没被定义。

推荐阅读：
[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)