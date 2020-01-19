---
title: node.js之stream流操作详细介绍——读出写入
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: node.js
cover: "/assets/images/blog-images/node/node-face.webp"
key: 2019121301
---

文件的写入 读出 属于Stream（流）。有可读，可写，可读可写和操作被写入数据，然后读出结果四种操作。
从流中读取数据首先要创建文件，并且写入一些可见的内容。

## 一、读取流

例如：

```
// Node.js Stream(流)
// 从流中读取数据
function ReadStream(){
var fs = require("fs");
var data = "";
// 创建可读流
var stream = fs.createReadStream("input.txt");
stream.setEncoding("UTF8");
// 处理流事件 --> data, end, and error
stream.on("data",function(chunk){
data+=chunk;
});
stream.on("end",function(){
console.log(c+data);
});
stream.on("error",function(err){
console.log("error"+err)
});
};
```



## 二、写入流

创建一个可以写入的流 不能用已经有内容的文档，文档会被清空重新写入；建议使用output.txt,会自动创建新的文件。

```
// 写入流
function WriteStream(){
let fs = require("fs");
let data = "人生的智慧";
// 创建一个可以写入的流 不能用已经有内容的文档，文档会被清空重新写入；建议使用output.txt,会自动创建新的文件
let writeStream = fs.createWriteStream("output.txt");
writeStream.write(data, "UTF8");

writeStream.end();
writeStream.on("finish",function(){
console.log("写入完成。");
});
writeStream.on("error",function(err){
console.log(err);
});
};
```


## 三、通道流

通道流就是连个文件之间接通，其中一个文件的内容跑到另外一个文件中去。相当于，读取一个文件内容并将内容写入到另外一个文件中。

```
// 管道流
function Pipe(){
let fs = require("fs");
var readerStream = fs.createReadStream("input.txt");
var writeStream = fs.createWriteStream("output.txt");

readerStream.pipe(writeStream); // pipe 表示流的吸管 readerStream流到writeStream中
console.log("end");

// 这个时候两个txt文件的内容是一样的
};
```



## 四、链式流

链式流就是通过连接输出流到另外一个流并创建多个流操作链的机制。比如压缩文件，就是通过读取文件，然后把问价写入到一个包里面，再压缩这个包。解压也是同样的原理，读取压缩包里面的文件，通过解压包，再写入到一个文件中。

例如：
```
// 链式流
// 压缩过程
function compress(){
let fs = require("fs");
let zlib = require("zlib"); // 压缩包

fs.createReadStream("input.txt")
.pipe(zlib.createGzip()) // 创建压缩
.pipe(fs.createWriteStream("input.txt.gz")); // 输出压缩包

console.log("文件压缩完成");

}

// 解压过程
function decompress(){
let fs = require("fs");
let zlib = require("zlib"); // 压缩包

fs.createReadStream("input.txt.gz")
.pipe(zlib.createGunzip()) // 创建解压
.pipe(fs.createWriteStream("input1.txt")); // 输出一个新的解压后的文件
console.log("文件解压完成");
}
// ReadStream();
// WriteStream();
// Pipe();
// compress();
decompress();
```

推荐阅读：

[JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.html)

[JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)


[JavaScript变量作用域及关系简明教程](https://muitlog.com/2019/12/10/JavaScript%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F.html)


[JavaScript常见操作字符串方法](https://muitlog.com/2019/12/06/javascript%E6%93%8D%E4%BD%9C%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

[if...else, if...if...else和if...else if的使用情况](https://muitlog.com/2019/12/06/ifelse-ififelseifelse-if.html)