---
title: vue组件component和模板template的区分
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/Vue封面.webp"
key: 2019121102
---

## 一、vue组件
我们在注册组件的时候一般是局部注册，在需要的页面引入组件文件。除非是使用率大的，就会在`main.js`中全部注册。

![](/assets/images/blog-images/VUE/vue组件与模版.png)

例如：
```

<div id="example">
<my-component></my-component>
</div>

</body>
<script type="text/javascript">
// 定义
var MyComponent = Vue.extend({
template: '<div>我是vue.js组件</div>'
})
// 注册
Vue.component('my-component', MyComponent)
// 创建根实例
new Vue({
el: '#example'
})
</script>
```


输出：我是vue.js组件





## 二、vue.js模版

模版是可以被浏览器直接解析的html语句，所以创建模版要比创建组件简单很多。定义模版时，我也建议把模版写出来，不要写到vue.js里面，这样需要修改模版的时候就直接修改，不用搞懂数据，看起来也清晰。
例如：

```
<template id="template">
<h1>vue.js模版</h1>
</template>
//创建模版

</body>
<script type="text/javascript">
var app=new Vue({
el:"#example",
data:{
},
template:"#template"//挂载模版
})
</script>

```



## 三、组件和模版之间的联系

通过上面的例子，我们会发现，组件中包含着模版。使用组件的时候就用到了组件里面的模版，更加整体，更加注重数据传递。注册的组件可以用组件名来做html标签，而模版是html代码块，更加注重样式。编写好的组件可以在多个页面调用，而模板在用的页面再重新编写，不能很好的实现复用。


推荐阅读：


[JavaScript面向对象编程及原型链理解【重点】](https://muitlog.com/2019/12/03/javascript.html)


[XMLHttpRequest对象原理和用法理解](https://muitlog.com/2019/12/02/xml-httprequest.html)


[JavaScript高阶函数常见用法大全](https://muitlog.com/2019/12/02/JavaScript%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0.html)


[ES6之Map与Set数据类型——快速查找键值](https://muitlog.com/2019/11/29/es6-map-set.html)


[ES6 块的作用域-let以及数组和字符串语法](https://muitlog.com/2019/11/28/es6-let.html)