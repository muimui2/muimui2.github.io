---
title: vue引入element-ui的流程和注意事项
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/成功界面.png"
key: 2019120502
---

初次使用vue搭建项目的时候，你也许不知道UI框架怎么引入，不用着急，下面来为你详细讲解。



## 一、安装element-ui

安装官方element-ui文档的安装方法安装。在npm中输入如下命令：
```
npm i element-ui -S
```

安装成功后就会发现就你的项目依赖目录下多了一个【element-ui】文件夹。因为文件太多了有点难找，直接搜就能搜出来，如果没有可以再执行一下上面的命令，因为我第一次也没安装成功呢。



## 二、引入

引入文件到相应的文件当中去，不过一般都是在main.js中全局引入，这样其他的文件不用多次引入也可以直接使用了。如图，是我在初次新建main.js中新增的语句，是引入element-ui的关键。

![](/assets/images/blog-images/VUE/引入element.png)

## 三、使用

到element-ui中复制一段html代码块过来测试一下，开始我是直接放在index.html中，发现是不行的，出错了。这就是我想说的重点，之所以出错是找不到模版吧。所以一定是要模版.vue后续的文件。所以我把代码复制到项目自带的测试文件【HelloWorld】中就可以了。


![](/assets/images/blog-images/VUE/首次错误信息.png)

![](/assets/images/blog-images/VUE/成功界面.png)


## 四、创建模版vue文件

上面的例子是拿项目原来就有的测试文件来用了，那怎么自己快速创建项目vue模版文件呢？

### 1、定义模版

按住【shift】+【ctrl】+p,调出控制台，在上面输入【snippet】回车，然后再输入vue，vscode会生成一个文件，这就是我们要创建模版的地方，不过里面的语句都是注释了的，我们可以自己添加进去自定义模版。
如下：

![](/assets/images/blog-images/VUE/生成模版命令.png)

```
"Print to console":{
"prefix": "vue",
"body": [
"<template>",
" <div class=\"wrapper\">$0</div>",
"</template>",
"",
"<script>",
"export default {",
" props: {",
" },",
" data () {",
" return {",
" }",
" },",
" created () {},",
" mounted () {},",
" watch: {},",
" computed: {},",
" methods: {},",
" components: {},",
"}",
"</script>",
"<style scoped>",
"</style>"
],
"description": "A vue file template"
```

### 2、新建vue文件

定义模版之后保存好，重启一下vscode，然后再【components】模版文件夹中新建文件，再新建的文件中输入vue然后直接按【TAB】键就生成了模版了。是不是很快呢，我也很喜欢用正方法。


![](/assets/images/blog-images/VUE/快捷新建模版.png)


推荐阅读：
[VUE模板语法快速入门教程](https://muitlog.com/2019/12/04/VUE%E6%A8%A1%E6%9D%BF%E8%AF%AD%E6%B3%95.html)


[VUE自定义指令图文解读](https://muitlog.com/2019/12/04/VUE%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8C%87%E4%BB%A4.html)


[vue element-UI实现分页查询](https://muitlog.com/2019/12/01/vue-element-ui.html)

[vue之Mixins混入结合图例易理解](https://muitlog.com/2019/11/29/vue-mixins.html)


[前端引入模板的4种方法](https://muitlog.com/2019/11/27/%E5%89%8D%E7%AB%AF%E5%BC%95%E5%85%A5%E6%A8%A1%E6%9D%BF%E7%9A%844%E7%A7%8D%E6%96%B9%E6%B3%95.html)