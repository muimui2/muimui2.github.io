---
title: vue之Mixins混入结合图例易理解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
cover: "/assets/images/blog-images/VUE/Vue封面.webp"
tags: vue
key: 2019112902
---

当页面的风格不用的时候，执行的方法和需要的数据类似，我们是选择每个都写呢还是提取出公共部分呢？这个时候就可以使用到vue中的混入了，混入Mixins是一种分发Vue组件中**可复用**功能的非常灵活的一种方式。当组件和混入对象含有同名选项时，这些选项将以恰当的方式混合。以下vue混入的例子和详细说明。


## 一、vue.js混入的基本用法

比如一个已经写好了的程序，每次点击都会增加1。现在想额外增加一个功能，可以在每次发生数据变化时都在控制台打印出来。
例如以下这个时间相互转换的例子：

```
<div id = "mixins">
<p>num:{{ num }}</p>
<P><button @click="add">增加数量</button></P>
</div>
<script type = "text/javascript">

var app=new Vue({
el:'#mixins',
data:{
num:0
},
methods:{
add:function(){
this.num++;
}
},
})
</script>
```



增加的vue.js混入如下：

```
<script type = "text/javascript">

var Mymixin={
updated:function(){
console.log("之前的数据是"+this.num+".");
}
}
var app=new Vue({
el:'#mixins',
data:{
num:0
},
methods:{
add:function(){
this.num++;
}
},
mixins:[Mymixin]//混入
})
</script>
```


![](/assets/images/blog-images/VUE/vue混入实例-01.webp)

以上就是一个简单的vue.js混入。






## 二、vue.js混入的逻辑顺序

如上例子，我的vue.js混入的对象名字是updated，如果我的vue.js混入对象的名字和组件的名字相同，会先执行那个呢？一般来说是按顺序执行的。在vue.js混入中，而当相同的对象名字在methods中，会以Vue 实例优先级会较高。

例如：

```
<script type = "text/javascript">

var Mymixin={
add:function(){
console.log("之前的数据是"+this.num+".");
}
}
var app=new Vue({
el:'#mixins',
data:{
num:0
},
methods:{
add:function(){
this.num++;
console.log("vue实例中打印"+this.num+".");
}
},
mixins:[Mymixin]//混入
})
</script>
```



![](/assets/images/blog-images/VUE/vue混入打印实例-02.webp)

vue.js混入的方法无法再执行，起不了作用。




## 三、vue.js混入全局混入

全局混入的意思自定义了一个全局的实例，如果需要这个混入功能直接new 	Vue({})创建实例对象就可以了。
```

Vue.mixin({
created: function () {
console.log("vue.js混入")
}
})

new Vue({})
```


以上是有关vue.js混入的实践操作和实例解析。简单说vue.js混入就是封装了方法的对象。在我们需要使用时就对象实例化。