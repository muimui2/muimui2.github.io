---
title: JavaScript初级教程——引入方式及调试方法
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
key: 2019121802
cover: null
tags: JavaScript
---

浏览器都内置JavaScript内核，所以使用JavaScript的时候，无需安装什么插件和第三方库，直接上手易学易操作，那么JavaScript应该写在页面的哪些地方？


## 一、JavaScript放置位置

### 1、写在头部

JavaScript可以直接嵌在html文件的`<head></head>`标签中，按照先后顺序执行。

例如：
```ruby
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>javascript学习教程</title>
<script type = "text/javascript">
console.log("hello javascript!")
</script>

</head>
<body>
</body>
</html>
```


### 2、在头部引入

JavaScript可以直接写在一个js文件格式里，在网页的头部或者或者尾部以src的形式引入。比较推荐用这种，可以使html内的代码保持整洁外，js文件也可以引入到其他文件中使用。

例如：
```ruby
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>javascript学习教程</title>
<script src="./javascript-01.js"></script>

</head>
<body>
</body>
</html>
```






## 二、JavaScript编写工具

其实可以用任何文件来编写JavaScript，如果只想编写JavaScript，只需要在编写完的文件改为.js格式的可以，那就是一个单纯的JavaScript文件了。

编写JavaScript的工具我强烈推荐Visual Studio Code，因为真的很轻便很好用，界面也很整洁智能。还可以在内部下载安装其他插件，都是自动化的，还可以当记事本使用。

另外就是webstorm，Notepad++等，我刚入门的时候用的是webstorm。

## 三、调试


调试可以在浏览器调试，F12会把调试界面调出来，或者【右键】浏览器【检查】然后可以在console中查看错误的代码和原因。可以在浏览器调试面板中会看到网页运行情况。
另外，console灵活使用的话，会大大提高调式效率


推荐阅读：

[JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.html)

[JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)


[JavaScript变量作用域及关系简明教程](https://muitlog.com/2019/12/10/JavaScript%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F.html)


[JavaScript常见操作字符串方法](https://muitlog.com/2019/12/06/javascript%E6%93%8D%E4%BD%9C%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

[if...else, if...if...else和if...else if的使用情况](https://muitlog.com/2019/12/06/ifelse-ififelseifelse-if.html)