---
title: 如何在HTML中使用JavaScript——前端新手
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: HTML JavaScript
cover: "/assets/images/blog-images/JS/在html中使用JavaScript.webp"
key: 2019111502
---

本章介绍< script >元素和< noscript >元素
JavaScript 是一种专为与网页交互而设计的脚本语言。下面来看一下在HTML中如何使用JavaScript 。

	
## 	一、< script>元素

![](/assets/images/blog-images/JS/在html中使用JavaScript.webp)
	
我们需要把JavaScript 代码写到`< script>`标签中才能被浏览器解析，除此之外`< script>`标签还有一个src属性，用于引用外部JS文件，scr属性的值用于存放外部文件的值得路径。

`<script type="text/javascript" src="example.js"></script> `


那么`< script>`在文档中的什么位置？
一般我们可以放在 `< head >< / head >`之间，那么问题来了，如果我们引用很多个外部文件或者写的代码块足够多那岂不是要等到`< script>`完全加载完成页面才开始显示？其实是的，使得页面还没加载完成的时候是空白的，所以我们要使用脚本的延迟加载或者是异步加载，延迟加载是defer属性，异步加载是async属性，`< script>`加上延迟加载属性defer的意思是在加载完成HTML之后才开始开始执行` < script>`下载，但是如果多个文件都加载了defer属性，那下载就不会分先后顺序的了，也不知是哪个先，那个后，所以这个时候要确保哪个文件需要延时加载，这里给一个文件添加这个属性比较好，而且，延时脚本defer只对外部引用的JS文件有效。对于写在`< script>`的代码块无作用。


加上异步加载属性async的意思是立刻开始下载 `< script>`文件，其实是会在页面加载之前执行。

	
这两个是脚本加载的方式，其实我们通常比较少用到，因为我们可以把脚本放在`</ body>`之前就可以了，加载完了HTML页面文件才开始下载< script>，就不需要管这两个属性了。

例如：

```
<html> 
<head> 
<title>JS</title> 
</head> 
<body> 
<script type="text/javascript" defer="defer" src="example.js"></script> 
</body> 
</html>
```




## 二、< noscript>元素

简单再说，`< noscript>`标签就是用来检测浏览器是否支持JS的，把HTML内容写到`< noscript>`标签里面，当浏览器不支持JS时就会显示`< noscript>`中的内容。

例如：

```
<html> 
<head> 
<title>noscript</title> 
<script type="text/javascript" defer="defer" src="example.js"></script> 
</head> 
<body> 
<noscript> 
<p>本页面需要浏览器支持（启用）JavaScript。
</noscript> 
</body> 
</html>
```