---
title: vue使用Ajax发送get和post请求的方法
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
key: 2019121702
tags: vue
---

因为vue.js中没有内置任何ajax请求方法。所以需要借助**第三方资源库**在发送ajax请求。比如[vue-resource资源库](https://github.com/pagekit/vue-resource)和[axios](https://github.com/axios/axios)。


## 一、资源库的安装和使用

使用vue-resource（vue1.0版本）、axios（vue2.0版本）等插件实现。

### 1、npm安装（二选一）

{% highlight ruby linenos %}
npm install axios 或者
npm install vue-resource
	
{% endhighlight %}


### 2、下载js资源文件
这里需要大家去找资源了。
	
### 3、通过script src的方式进行文件的引入（二选一）

国内的CDN优先，比如：[bootcdn](https://www.bootcdn.cn/)
再推荐一个国外的：[cdnjs](https://cdnjs.com/)


{% highlight ruby linenos %}
<script src="https://cdn.staticfile.org/vue-resource/1.5.1/vue-resource.min.js"></script>//或者
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

{% endhighlight %}


## 二、语法

### 1、全局对象方式 Vue.http发起http请求

{% highlight ruby linenos %}
Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);
Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);

{% endhighlight %}



### 2、Vue 实例中使用 this.$http发起http请求


{% highlight ruby linenos %}
this.$http.get('/someUrl', [options]).then(successCallback, errorCallback);
this.$http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);

{% endhighlight %}

除了`get`,`post`外，还有其他的http请求数据方法，例如：head，delete，put，语法都是一样的。


## 三、在vue项目中使用get请求


### 1、读取数据

{% highlight ruby linenos %}
<div id="box">
    <input type="button" @click="get" value="点我异步获取数据(Get)">
</div>
<script type = "text/javascript">

window.onload = function(){
var vm = new Vue({
el:'#box',
data:{
},
methods:{
get:function(){
//发送get请求
this.$http.get('https://api.apiopen.top/recommendPoetry').then(function(res){
document.write(res.body.result.content); 
console.log(res)//查看api数据结构
},function(){
console.log('请求失败处理');
});
}
}
});
}
</script>
{% endhighlight %}

![](/assets/images/blog-images/VUE/vue-get请求-01.png)


### 2、传递数据
语法：`get(‘url地址’,{ jsonData});`

第二个参数是json个是的数据。
例如：

{% highlight ruby linenos %}
<script type = "text/javascript">

window.onload = function(){
var vm = new Vue({
el:'#box',
data:{
},
methods:{
get:function(){
//发送get请求
this.$http.get('https://api.apiopen.top/recommendPoetry',{body:{result:{title:"用文之韵赋岩桂"},result:{authors:"张扩"}}}).then(function(res){
document.write(res.body.result.content); 
console.log(res)//查看api数据结构
},function(){
console.log('请求失败处理');
});
}
}
});
}
</script>
{% endhighlight %}



## 四、在vue.js中使用post请求
post发送数据需要第三个参数。
语法：`post('url地址',{json数据},{emulateJSON:true})`
emulateJSON 的作用： 如果Web服务器无法处理编码为 application/json 的请求，你可以启用 emulateJSON 选项。

例如：

{% highlight ruby linenos %}

window.onload = function(){
var vm = new Vue({
el:'#box',
data:{
},
methods:{
post:function(){
//发送get请求
this.$http.post('https://api.apiopen.top/recommendPoetry',{result:{title:"用文之韵赋岩桂"},result:{authors:"张扩"}},{emulateJSON:true}).then(function(res){
document.write(res.body.result.content); 
console.log(res) 
},function(){
console.log('请求失败处理');
});
}
}
});
}
</script>

{% endhighlight %}




## 五、发送跨域请求

跨域请求是，由于浏览器同源策略，凡是发送请求url的协议、域名、端口三者之间任意一与当前页面地址不同的请求即为跨域请求。

如下：属于同域的不同文件，是允许通讯的，不存在跨域。


{% highlight ruby linenos %}
http://www.xx.com/a.js
http://www.xx.com/b.js
{% endhighlight %}



同一域名不同端口，不允许通讯，如果要通讯存在跨域。

{% highlight ruby linenos %}

http://www.xx.com:8080/a.js
http://www.xx.com/b.js
{% endhighlight %}

同一域名不同协议，不允许通讯，如果要通讯存在跨域。

{% highlight ruby linenos %}

http://www.xx.com:8080/a.js
https://www.xx.com/b.js
{% endhighlight %}

域名不同，不允许通讯，如果要通讯存在跨域。

{% highlight ruby linenos %}

http://www.xx.com:8080/a.js
http://www.jj.com/b.js
{% endhighlight %}

本文结合实例粗略的讲解了一下vue.js中使用Ajax的get和post请求和发送数据的方法，是大家能更容易的理解和使用。
在本文的上面例子都是跨域发送请求，因为我使用的都是外部的API做测试使用。具体项目情况把你要请求的连接替换即可。希望可以帮到你。