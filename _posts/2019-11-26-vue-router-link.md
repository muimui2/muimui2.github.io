---
title: vue router-link属性集合详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/Vue封面.webp"
key: 2019112601
---

路由就相当于`< a> </ a>` 标签中的href 也就是负责页面的跳转活动，在本章我们再学习详细学习vue路由的作用和用法。

vue路由需要使用 `router-link `组件来导航，那么`router-link`包含哪些属性呢？这些属性又有什么作用呢？我们一起来学习路由的属性和特性。

![](/assets/images/blog-images/VUE/Vue封面.webp)


## 一、to属性

在vue路由中，to 表示目标路由的链接。当被点击后，内部会立刻把to的值传到`router-push()`，值可以是一个字符串或者是描述目标位置的对象。进行路径的跳转。`< router-link>` 默认会被渲染成一个 `<a>` 标签，to相当于a标签中的"herf"属性，后面跟跳转链接所用，被渲染成：
	
```
< a href="#foo1"></a>

//上述代码等同于:

<router-link :to="{path: 'foo1'}" >路由1</router-link>
```


如图：

![](/assets/images/blog-images/VUE/vue路由to属性实例-01.webp)




## 二、replace属性

在javascript语法中，`replace() `方法用于在字符串中用一些字符替换另一些字符，是替换方法。而在vue中会不会有什么不同呢。在vue中，设置这个属性其实也是替换的作用，会调用 `router.replace()` 而不是 `router.push()`，作用是导航后不会留下 history 记录。

用法：

`<router-link to="/foo1" replace>路由1</router-link>`




## 三、tag

我们知道，`< router-link>`会被渲染成a标签，但是要想被渲染成其他标签，有没有办法呢？`Tag`是标签的意思，设置了`tag`属性，`router-link`会被渲染成相应的标签，同样它还是会监听点击的功能。

例如：

```

<router-link to="/foo1" tag='li'>路由1</router-link>
```


![](/assets/images/blog-images/VUE/vue路由tag属性实例-02.webp)


## 四、active-class

设置`active-class`属性是当`router-link`中的链接被激活是，添加css类名。也就是当前页面所有与当前地址所匹配的的链接都会被添加class属性。如果没有设置`active-class`属性，vue会有一个默认的class来表示当前链接被激活：`router-link-active`。

```
<router-link active-class='active_class' :to="{path: 'foo1'}" >路由1</router-link>

```


![](/assets/images/blog-images/VUE/vue路由active-calss属性实例-03.webp)

## 五、exact-active-class

`exact-active-class`和`active-class`相类似，不同的是，exact-active-class是配置当链接被精确匹配的时候应该激活的 class。不设置的时候，默认的class：`router-link-exact-active`

```
<router-link active-class='active_class' exact-active-class = "_active" :to="{path: 'foo1'}" >路由1</router-link>

```


## 六、event

event属性是声明可以用来触发导航的事件，event的值可以是一个数组或者一个字符串。

用法：
```

<router-link to="/foo2" event='mouseover'>点击2</router-link>
```


添加属性后把鼠标放上去不用点击都会发生跳转哦。

以上是学习router-link的属性，方法和使用实例。除此之外，在实际项目中，其实更多用到的是配置路由的功能，路由配置文件中加入路由，然后vue组件中调用。待续，我将在下节中讲到。