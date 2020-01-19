---
title: 没有dev-server.js文件如何mock数据
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
key: 2019121901
cover: /assets/images/blog-images/VUE/Vue封面.webp
---

在学习vue的时候，想要模拟数据。可以通过外部api，也可以自己写一些json格式的数据。可是具体要写在什么文件呢？

## 一、定义数据和引入数据

我们可以在dev-server.js文件中定义数据和引入数据，可是我新建的项目中找不到这个文件？原来，更新了!!!新版本的vue项目中没有dev-server.js文件了，被webpack.dev.config.js代替了，所以我们现在是要在webpack.dev.config.js文件中定义数据和引入数据。
例如：
```ruby
const portfinder = require('portfinder')
//在这里开始定义数据和引入数据
const express = require('express')
const app = express()
var appData = require('../data.json')//加载本地数据文件
var apiRoutes = express.Router()//创建路由
app.use('/api', apiRoutes)//’/api’是路由的路径
```


## 二、mock数据

通过第一步定义好数据和引入数据后，我们现在要对数据文件做返回数据的操作，同样也是在`webpack.dev.config.js`文件中，找到`devServer：{ }`，我们把数据的获取写在里面。我们要用`get（）`方法获得返回的数据，`get（）`携带两个参数，第一个是路由得路径，第二个是返回数据的方法。
例如：
```ruby
devServer: {
//开始mock数据
before(app) {
app.get('/api/appData', function(req,res) {
res.json({
errno: 0,
data: appData
})//接口返回json数据，上面配置的数据appData就赋值给data请求后调用
})
},
```

最后可以试一下，是不是取得了返回了json格式的数据，由于我是本地的项目，所以我的地址是http://localhost:8085/api/appData。
不过我们在开发项目过程中，都是从后端获取数据的。所以这个比较适合在学习或者练习的时候使用。

推荐阅读：
[vue使用Ajax发送get和post请求的方法](https://muitlog.com/2019/12/17/vueajaxgetpost.html)

[3种vue元素绑定事件方法详解](https://muitlog.com/2019/12/17/3%E7%A7%8Dvue%E5%85%83%E7%B4%A0%E7%BB%91%E5%AE%9A%E4%BA%8B%E4%BB%B6.html)

[手机测试vue项目](https://muitlog.com/2019/12/13/%E6%89%8B%E6%9C%BA%E6%B5%8B%E8%AF%95vue%E9%A1%B9%E7%9B%AE.html)

[7步搭建vue项目环境——多图慎点](https://muitlog.com/2019/12/12/7vue.html)

[vue使用v-if...v-else...详解](https://muitlog.com/2019/12/11/vue-v-ifv-else.html)