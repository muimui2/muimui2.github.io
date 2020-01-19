---
title: Node.js之readFileSync,EventEmitter和Buffer
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: node.js
cover: "/assets/images/blog-images/node/node-face.webp"
key: 2019121303
---

## 一、阻塞代码

因为代码是从上到下执行的，所以没有特殊情况的话，前面的如果有复杂的程序耗时长，只能等待前面的先执行，再执行后面的，形成了阻塞代码。exports 是模块公开的接口(对象)。

{% highlight ruby linenos %}
// 阻塞代码实例 按照顺序执行，不管前面的有多复杂，所以为阻塞代码
var fs = require("fs");

var data = fs.readFileSync('input.txt');

console.log(data.toString());
var time = new Date;
var n = time.getHours();
console.log(n);
// 月亮与六便士
// 17
{% endhighlight %}


## 二、非阻塞代码

想要非阻塞程序的话，就要使用回调函数，回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

{% highlight ruby linenos %}
// 非阻塞代码实例 首先执行了输出日期，等待readFile执行完毕后再输出结果。
var fs = require("fs");
fs.readFile("input.txt",function(err,data){
    if(err) {
        console.log(err);
    }
    console.log(data.toString());
})

var time = new Date;
var n = time.getHours();
console.log(n);
// 17
// 月亮与六便士

{% endhighlight %}

以上就是node学习回调函数的重点。


## 三、EventEmitter 类

Node.js的events时间模块提供了events.EventEmitter对象，用于事件触发与事件监听器功能的封装。通过require("events");访问该模块。


{% highlight ruby linenos %}
// 触发和监听事件
var events = require('events'); // 引入模板 
var EventEmitter = events.EventEmitter; // 创建 EventEmitter 对象
var event = new EventEmitter(); // EventEmitter对象实例化

// 定义函数
function sayHi(){ 
console.log("Hi MUIMUI");
};

function sayBye(){ 
console.log("Bye MUIMUI");
};

function sayHello(){ 
console.log("sayHello MUIMUI");
};

// 可以出发多个事件

event.on("say",sayHi); // on 绑定时间，第一个参数为绑定时间的名称，第二个为时间函数
event.on("say",sayBye); // on 绑定时间，第一个参数为绑定时间的名称，第二个为时间函数

// once(event, listener) 只触发一次监听，触发后立即解除监听
event.once("say",sayHello);

// 移出监听事件
event.removeListener("say",sayHello);

// listeners 返回事件的监听器数组
var arr = event.listeners("say");

// listenerCount 返回指定事件的监听器数量。
var count = event.listenerCount("say");

setTimeout(function(){
// emit 触发事件 参数为时间的名称
event.emit("say");
console.log(arr); // [ [Function: sayHi], [Function: sayBye] ]
console.log(count); // 2
},1000);

{% endhighlight %}


## 四、Buffer 与字符编码

因为JavaScript有字符串类型，而计算机是读取二进制文件，所以需要一个缓冲区，把字符串类型转为二进制文件。
Buffer 实例一般用于表示编码字符的序列，比如 UTF-8 、 UCS2 、 Base64 、或十六进制编码的数据。可以和 JavaScript 字符串之间进行相互转换。
例子：



{% highlight ruby linenos %}

// 缓冲区 字符编码 
// Buffer.from接口 创建Buffer对象。
// 创建一个长度为 256、且用 0 填充的 Buffer。

var buffer = Buffer.alloc(10); 

// 写入缓冲区
var b = buffer.write("muimui");

// 将 Buffer 转换为 JSON 对象
var json = JSON.stringify(buffer);

// JSON.parse() 方法将数据转换为 JavaScript 对象
var strObj = JSON.parse(json,function(key,value){
return value;
}); 

console.log(strObj.data); // [ 109, 117, 105, 109, 117, 105, 0, 0, 0, 0 ]

// 缓冲区合并
var buffer1 = Buffer.from("muimui");
var buffer2 = Buffer.from("hello");
var buffer3 = Buffer.concat([buffer1,buffer2]);

console.log(buffer3); // <Buffer 6d 75 69 6d 75 69 68 65 6c 6c 6f>

setTimeout(function(){
// base64
console.log(buffer.toString("base64"));
// utf8
console.log(buffer.toString("utf8"));
console.log(b); // 输出： 6 表示字节为6
// 从缓冲区读取数据 buf.toString([encoding[, start[, end]]])
console.log(buffer.toString("utf8",0,3)); // 输出：mui

},1000);

{% endhighlight %}

以上是关于node.js的回调函数，EventEmitter监听类，和缓冲区Buffer的学习。