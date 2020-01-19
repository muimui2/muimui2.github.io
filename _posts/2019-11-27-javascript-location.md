---
title: JavaScript之location常用属性大全
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019112703
---

location是JavaScript的BOM对象之一，既是window对象的属性，JavaScript的Location对象有什么用？提供与当前窗口中加载的文档有关的信息和提供导航功能。


location 也有很多属性，今天就来总结一下。
例如有这要一地址字符串：
http://localhost:8080/#/manageCenter/videoManage?nonc_str=1574843641252



## location.hash

返回URL中的#号后的多个字符，如果URL中不包含散列 ，则返回空字符串。

```
#/manageCenter/videoManage?nonc_str=1574843641252
```



## location.host

返回服务器名称+端口号

```
localhost:8080
```

## location.hostname

返回不带端口号的服务器名称

```
localhost
```


## location.href

返回当前加载页面的完整URL 。
例如：
```

location.toString() == location.href   //true

 http://localhost:8080/#/manageCenter/videoManage?nonc_str=1574843641252

```

## location.pathname

返回URL中的目录+文件名

```
/
```

## location.port

返回端口号，如果没有端口号返回空字符串

```
8080
```

## location.protocol
返回使用的协议http or https

```
http:
```

## location.search
返回URL中的查询字符串，这个字符串以问号开头

```
//没有值
```

## location.origin

返回URL协议+服务器名称+端口号  
例如：
```

location.origin == location.protocol + '//' + location.host

http://localhost:8080

```