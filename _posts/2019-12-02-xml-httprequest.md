---
title: XMLHttpRequest对象原理和用法理解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/XHR原理图.webp"
key: 2019120202
---

Ajax技术的核心是XMLHttpRequest对象，简称：XHR。别看名字中包含XML，其实和数据格式无关，重点是无需刷新页面都可以从服务器获取数据，数据格式不一定是XML。本章要来详细理解web世界传输数据的规则，区分和用法，即是XMLHttpRequest对象原理和用法理解。




## 一、XHR的用法

XHR发展至今，大多数浏览器都已经开始支持XHR，但IE7之前的版本是不支持的，但是所有浏览器都有MSXML库，所以我们要告诉浏览器根据MSXML库中的一个ActiveX对象实现。在使用XHR的时候需要创建XHR实例对象。
例如：
```
var xhr=new XMLHttpRequest();

```

在使用XHR对象是，需要调用一个`open（）`方法，`open（）`方法接受三个参数，第一个参数是发送的方式；第二个是请求的页面；第三个是一个布尔值，表示是否异步发送请求，如果异步则为“true”，否则为“false”。同事要调用一个send（）发送方法，这个方法接收一个参数，是发送到服务器的请求数据，如果没有发送数据，就填写“null”，因为有些浏览器这里必须得有个值，否则可能就有问题了。
例如：
```
xhr.open("GET","https://api.apiopen.top/recommendPoetry",falese);
xhr.send(null);
```

发送请求之后，服务器都对其做出响应。响应的结果会自动添加到XHR的属性值那里去。一般而然，http的状态码是200标示已经响应成功。

除此之外，XHR还有一个属性是readyState，readyState属性有0-4这五个值，分别用来标示请求和响应过程中当前的活动状态。0-4这四个阶段中，当readyState的值为4时，表示数据已经返回到浏览器啦，可以在浏览器中使用数据啦。不过使用readyState之前，需要在open（） 之前指定onreadystatechange事件在检测readyState状态。

![](/assets/images/blog-images/JS/XHR原理图.webp)

例如：
```
var xhr;
if (window.XMLHttpRequest)
{// code for IE7+, Firefox, Chrome, Opera, Safari
xhr=new XMLHttpRequest();
}
else
{// code for IE6, IE5
xhr=new ActiveXObject("Microsoft.XMLHTTP");
}
xhr.onreadystatechange=function()
{
if (xhr.readyState==4 && xhr.status==200)
{
console.log(xhr.responseText);//返回的数据文本
}
}
xhr.open("GET","https://api.apiopen.top/recommendPoetry",true);
xhr.send(null);
```

以上代码返回的是一个json格式的对象，当我想访问对象属性的时候发现是“undefined”为什么呢？原来是字符串类型了。要转为object格式才可以访问对象属性。
```
console.log(typeof(JSON.parse(xhr.responseText)));//object类型
console.log(typeof(xhr.responseText));//string类型


```



## 二、HTTP头部信息

在请求和响应都会有响应的HTTP头部信息，客户端向服务器发送一个请求，请求头包含请求的方法、URI、协议版本、以及包含请求修饰符、客户信息和内容的类似于MIME的消息结构。服务器以一个状态行作为响应，相应的内容包括消息协议的版本，成功或者错误编码加上包含服务器信息、实体元信息以及可能的实体内容。XHR中有三个方法是处理头部信息的：
```
setRequestHeader（“myheader”,”myvalue”）;设置头部信息，带两个参数，第一个是头部信息的名称，第二个是需要设置的值。
getRequestHeader(“myheader”);获得头部的信息，带一个参数，该参数标示需要获取的头部信息的名称，返回值。
getAllRequestHeaders( );不带参数，返回全部头部信息。

例如：
xhr.open("GET","https://api.apiopen.top/recommendPoetry",true);
xhr.setRequestHeader('myname','myname');
xhr.send(null);
```






## 三、GET请求

GET请求是常见的请求类型，是页面向服务器请求数据的方法，请求的形式是在url连接上带参数，通常参数是放在url的末尾，并且每一对名-值的参数都要用和好“&”分开。可是有些请求的页面的url是没有问号“？”的，我们需要加上问号才能添加参数。如下例子中我们定义了一个函数，用于判断连接中是否有问号，“-1”表示找不到索引，用三元运算给连接url加上问好“？”，如果存在问号表示已经带了一个参数了，就给链接url加上“&”和参数隔开。
例如：
```
function addurl(url,name,val){
url = url + (url.indexOf("?") == -1 ? "?" : "&");
url = url + name +"="+ val; 
console.log(url)//https://api.apiopen.top/recommendPoetry?page=1 在url后面添加参数
}
var href = "https://api.apiopen.top/recommendPoetry";
addurl(href,"page","1");
```

如果出现加入的参数有格式的问题，需要给参数的每个名字和值使用encodeURIComponent( ) 函数可把字符串作为 URI 组件进行编码，例如：`encodeURIComponent(name)`。反正我没遇到过这样的问题，如果你遇到了这样可以解决。 



## 四、POST请求

GET提交虽然简单，查询字符串只需要以参数的形式加到url提交就可以了，那么简单你以为不用付出代价么，相对于POST而然，代价就是不够安全，会把你请求的数据暴露出来让大家都能看见，并且请求的参数是有限的，浏览器通常都会限制url长度在2K个字节，不过你不介意就没关系。所以我个人会用POST请求比较多，因为在实际项目中，不可能把用户的信息暴露出来，并且要提交的数据一般都比较多，用POST是最适合的选择，而且也不难，就是把open( )方法中的第一个参数换成POST就可以初始化一个POST请求了。另外因为send( )是发送数据到服务器的，所以可以在这里加入一个XML格式的文档，为什么GET不行，因为GET发送携带的数据有限啊，适合少量发送，而POST可以把一整个文档都发送过去。所以可以用于提交表单文件等。
另外，既然`send( )`中装载着数据，所以使用`POST`时要注意设置`Content-Type`的内容为`application/x-www-form-urlencoded`，用于告诉服务器请求有参数变量。以便浏览器出来迎接数据。所以，GET产生一个TCP数据包；POST产生两个TCP数据包。
例如：
```
xhr.open("post","https://api.apiopen.top/recommendPoetry",true);
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send("page=1");

```



推荐阅读：

[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)