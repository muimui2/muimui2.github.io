---
title: vue过滤器filters结合实例解析
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/filters过滤器.webp"
key: 2019111804
---

在一开始使用vue的时候，也许你还不够熟悉，觉得vue是在有太多的属性了，不知道函数应该写在哪个方法下面，为了快速的使用vue，拽这里可以区分：[VUE框架属性方法图文全解](https://muitlog.com/2019/11/17/VUE%E6%A1%86%E6%9E%B6%E5%B1%9E%E6%80%A7%E6%96%B9%E6%B3%95%E5%9B%BE%E6%96%87%E5%85%A8%E8%A7%A3.html)

这个结合例子详细解析以下过滤器filters，一开始理解过滤器的时候以为是过滤不要的内容，原来再vue中，过滤器有承接的关系，就是上一个过滤器的返回值给下一个过滤器，下一个过滤器的返回值给下下一个过滤器...

图解：

![](/assets/images/blog-images/VUE/filters过滤器.webp)

filters过滤器会把第一个前一个变量的值拿过来作为函数的变量。本例子中message是一个数字，作为filter（）的变量。
例如:

```
<div id="app">
<span>{{message | filter | filter | filter}}</span>
</div>
<script>
var vue = new Vue({
el:'#app',
data:{
message:"10"
},
filters:{
filter(val){
return val*10; // 10000
}
}
})
</script>
```