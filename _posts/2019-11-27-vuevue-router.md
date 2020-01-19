---
title: vue如何创建路由vue-router
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/vue创建路由.webp"
key: 2019112707
---

我们更多的是在项目中使用路由，安装路由和配置路由`vue-router`，在之前的文章中我们讲到[vue router-link属性集合详解](https://muitlog.com/2019/11/26/vue-router-link.html)那只是路由标签标签`router-link`的属性和使用。这章一起来安装配置vue路由。

## 一、什么是路由

刚开始听到这个名称的时候，老实说，其实我并不懂，好像家里使用的网络也有个叫路由的东西。经过请教，没错，vue.js路由就是和家里正在使用的路由是一样的道理，路由就是数据经过的关口，起到监控数据的作用。这样说是不是就明白多了。Vue.js 路由允许我们通过不同的 URL 访问不同的内容，就是在一个单页面内实现多视图的单页Web应用。



## 二、vue.js路由安装

路由需要安装，所以其实vue.js路由是一个外部的插件。如果没引入相关资源是使用不了路由的。引入的方式和引用vue.js一样。可是是CDN和npm指令下载。

```
//CDN:

<script src="https://cdn.staticfile.org/vue-router/2.7.0/vue-router.min.js"></script>

//Npm：
cnpm install vue-router
```


其实以前我做web端项目的时候，用的都是html静态页面，那时候喜欢用CDN，使用起来简单省事，可是现在我们新建一个项目的时候，用的都是vue ，这样话就要使用npm安装，可以确保文件的正确引入，还可以按需要查看文件的结构。

如果在一个模块化工程中使用vue.js路由，则要通过 Vue.use() 明确地安装路由功能。

例如：

![](/assets/images/blog-images/VUE/vue创建路由.webp)

```
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

```


## 三、Vue.js路由的使用

经过上面的介绍已经明白什么是路由，也明白使用之前的安装方法，那让我们一起来看看路由的使用，以便我们能马上使用vue.js路由。然后我们来看看创建vue.js路由的原理。


在创建路由之前，我们需要vue.js路由得入口和出口，路由出口就是路由渲染的地方，所以是写在html模版中。


```
<div id="app">
    <router-link to="/foo1">路由1</router-link>
    <router-link to="/foo2">点击2</router-link>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
</div>
```


我们在创建路由时，我们要创建一个组件，用于路由指定访问的模版。这里我为了演示，就把模版写在同一件文件中，不过是隐藏的状态。因为最终映射的是模版里面的 `< h1>`，所以这个样式是不会影响的。

```
<div id="template1" style="display: none">
    <h1>大家好，我是路由模版1</h1>
</div>
<div id="template2" style="display: none">
    <h1>我是路由模版2</h1>
</div>

const Foo1 = { template: '#template1' }
const Foo2 = { template: '#template2' }
```


有个路由模版，然后要定义一个路由。
例如：

```
const routes = [
    { path: '/foo1', component: Foo1 },
    { path: '/foo2', component: Foo2 }
]
```


路由是一个数组，里面可以包含着路由对象，`{ path: '/foo', component: Foo }`，对象包含两个参数，`/foo`是一条路由的`key`，它表示路径；`{component: Foo }`则表示该条路由映射的组件。



定义了路由，要创建 router 实例，调用构造器VueRouter，创建一个路由器实例router。

```
const router = new VueRouter({
    routes // （缩写）相当于 routes: routes
})
```

路由需要载到根实例上显示，在页面上使用`<router-view></router-view>`标签，它用于渲染匹配的组件。

```
const app = new Vue({
    router
}).$mount('#app')
```