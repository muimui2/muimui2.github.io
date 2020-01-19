---
title: JavaScript中级教程——对象的创建，访问和操作全解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019122001
cover: /assets/images/blog-images/JS/JavaScript封面.webp
---


JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...此外，JavaScript 允许自定义对象。

## 一、对象的语法

用`{ }`把键值对包起来，键值对以`xxx: xxx`形式申明，用【，】隔开，最后一对后面不用加【，】否则低版本的浏览器会认为对象属性还没书写完毕，会报错。

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
```

## 二、访问对象属性

有两种访问的方法。

### 【1】对象名.属性来访问

我们可以通过 对象名.属性来访问。因为这个属性属于这个对象，因此可以使用该方法。
例如：
```ruby
console.log(project.name)//小明
console.log(project.age)//18
```

你也许会发现，为什么‘best-friend’属性要用引号‘’括起来呢？因为属性中包含了特殊字符

### 【3】对象名[‘属性’]的方式来访问
基于以上的例子，所以可以使用对象名[‘属性’]的方式来访问

例如：
```ruby
console.log(project['best-friend']);//小红
console.log(project['address']);//北京路
```

使用哪种你随意。其实我们更多是使用第一种。

## 三、操作对象

怎么对对象的属性和属性值进行修改呢？由于JavaScript的对象是动态类型，所以既然可以访问到属性，那当然可以修改，增加属性和删除属性。
例如：小明改名字了，他最好的朋友也不是小红了，他没朋友了，转校了。
```ruby
console.log(project.name='罗小明');//修改
delete project['best-friend'];//删除
project['new-school']='新东方';//新增
console.log(project);
```


## 四、查询对象属性

加入一个对象的属性太多了，我们需要检测某个属性在不在这个对象内，我们可以用 in 来检测。
例如：
```ruby
console.log('name' in project)//true
console.log('page' in project)//false
```

但需要注意的是，用 in 方法检测到的属性有可能不是改对象的，有可能是该对象继承得到的。
例如：
```ruby
console.log('toString' in project)//true
```

为了解决这个问题，JavaScript提供hasOwnProperty( )方法来查询对象的属性是否是它自己的，而不是继承的。
例如：
```ruby
console.log(project.hasOwnProperty('toString'));//false

```


推荐阅读：

- [移动端访问PC链接自动切换链接地址](https://muitlog.com/2019/12/19/自动切换pc和移动端.html)
- [JavaScript中级教程—— JavaScript 数组操作总结](https://muitlog.com/2019/12/19/JavaScript数组操作总结.html)
- [JavaScript初级教程——引入方式及调试方法](https://muitlog.com/2019/12/18/javascript-引入方式及调试方法.html)
- [JavaScript初级教程——基本语法和注意事项](https://muitlog.com/2019/12/18/javascript-基本语法和注意事项.html)
- [javascript历史以及ECMAScript理解](https://muitlog.com/2019/12/16/javascript历史.html)





