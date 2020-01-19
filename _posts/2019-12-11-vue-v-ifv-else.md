---
title: vue使用v-if...v-else...详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/Vue封面.webp"
key: 2019121103
---

自从学习了vue之后，就基本把jquary舍弃了，因为jquary主要是处理DOM比较出色，不过vue连DOM都不用处理，直接处理数据就行了，如果需要判断元素，使用v-if...v-else...。

例如：
```
<div id="example-if">
<div class="div-A" v-if='Math.random()>0.5'>
显示代码块A
</div>

<div class="div-B" v-else>
显示代码块B
</div>
</div>
<script type = "text/javascript">
var vm = new Vue({
el: '#example-if',
data: {
}
});
</script>
```


不断刷新，你会发现随着随机数的变化，两个代码块也交替显示隐藏。


多个条件判断也是如此：
```
<div id="example-if">
<div class="div-A" v-if='message==="A"'>
显示代码块A
</div>

<div class="div-B" v-else-if='message==="B"'>
显示代码块B
</div>
<div class="div-C" v-else>
显示代码块C
</div>
</div>
<script type = "text/javascript">
var vm = new Vue({
el: '#example-if',
data: {
message:'C'
}
});
</script>
```



这里要注意的是，v-if是惰性的，没满足条件就不会渲染，不同于v-show。


推荐阅读：


[JavaScript面向对象编程及原型链理解【重点】](https://muitlog.com/2019/12/03/javascript.html)


[XMLHttpRequest对象原理和用法理解](https://muitlog.com/2019/12/02/xml-httprequest.html)


[JavaScript高阶函数常见用法大全](https://muitlog.com/2019/12/02/JavaScript%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0.html)


[ES6之Map与Set数据类型——快速查找键值](https://muitlog.com/2019/11/29/es6-map-set.html)


[ES6 块的作用域-let以及数组和字符串语法](https://muitlog.com/2019/11/28/es6-let.html)