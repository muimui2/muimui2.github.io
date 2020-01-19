---
title: 使用JavaScript操作DOM结构
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript中DOM操作.webp"
key: 2019111601
---

相信现在你已经很少用JavaScript来操作DOM元素，因为现在除了又vue，还有jquary，所以你很少会用到完全纯JavaScript在操作DOM，但是不怕一万就怕万一，如果你点开这篇文章，证明这正是你需要的。


DOM是文档对象模型，也就是引用程序接口，这个接口针对HTML或者是XML的，我们知道在我们的文档页面中，是以树节点的形式呈现的，所以当我们要获取，增加，或者删除其中的节点的时候，我们应该怎么做？我们的JS为我们提供了节点层次和DOM处理技术。让我们一起来看一下吧。


![](/assets/images/blog-images/JS/JavaScript中DOM操作.webp)

## 一、节点层次

节点层次可以分为九种类型，每个节点都拥有它特定的方法和特点，而且节点与节点之间都有某种关系。有的节点以节点之间构成树结构，所以文档节点就是说这个文档的根节点。以我们的html文档为例,html元素标签就是这个文档的根节点。



## 二、DOM操作技术

以上的九个节点就是为DOM操作提供方便,使得DOM操作比较简明。我们DOM操作的时候是通过在脚本上完成的，那怎么用同样的方法处理脚本呢。


### 1.动态脚本

引入脚本有两种方式，插入外部文件和直接插入JavaScript代码。
以下这个方法是动态新建和加载外部文件。这里我写了一个方法，把它封装起来。
例如：

```
function loadScript(url){ 
var script = document.createElement("script"); 
script.type = "text/javascript"; 
script.src = url; 
document.body.appendChild(script); 
}
loadScript("client.js");
```


另外一个方法就是动态加载脚本代码。考试在这里ie浏览器它不允许DOM访问指节点。所以要使用text属性来指定JavaScript代码。所以我们在这里就要分情况啦。下面封装了一个方法,需要动态加载的脚本代码，就以字符串的形式作为参数。

例如：
```

function loadScriptString(code){ 
var script = document.createElement("script"); 
script.type = "text/javascript"; 
try { 
script.appendChild(document.createTextNode(code)); // 可以DOM访问节点浏览器。
} catch (ex){ 
script.text = code; // 不可以访问节点的浏览器,使用text来指定代码，因为脚本代码就是script标签的文本。
} 
document.body.appendChild(script); // 加到document文档中
} 

loadScriptString("function sayHi(){alert('hi');}");
```




### 2.动态样式

动态加入样式也是有两种方法，外部加载文件和动态创建元素。在这里，动态加载外部文件就不多说啦，和上面动态加载脚本文件是一样的道理。需要注意的是，动态创建样式，需要把链接加到头部元素标签head里面。所以我们还要取到head标签的位置，再在头部head的位置上加链接。
同样的，如果动态加载样式代码，在ie浏览器中，也是不允许访问子节点的，会抛出错误，所以在这里我们要分情况。在这里我们使用样式表styleSheet的cssText属性。
```

function loadStyles(url){ 
var link = document.createElement("link"); 
link.rel = "stylesheet"; // 文件样式表。
link.type = "text/css"; // 类型
link.href = url; // 文件路径。
var head = document.getElementsByTagName("head")[0]; // 第一个头部文件的位置。
head.appendChild(link); // 把链接加到头部标签里面。
}

loadStyles("styles.css");


function loadStyleString(css){ 
var style = document.createElement("style"); 
style.type = "text/css"; 
try{ 
style.appendChild(document.createTextNode(css)); // 在除了ie浏览器的其他浏览器中
} catch (ex){ 
style.styleSheet.cssText = css; // 在ie浏览器中。
} 
var head = document.getElementsByTagName("head")[0]; 
head.appendChild(style); 
}
```