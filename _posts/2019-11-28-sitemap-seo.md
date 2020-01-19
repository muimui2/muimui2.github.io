---
title: 自动生成网站地图sitemap——SEO提高收录
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: SEO
key: 2019112805
---

因为想要博客被收录的话就要网站地图，Sitemap（即站点地图）就是您网站上各网页的列表。创建并提交 Sitemap 有助于百度发现并了解您网站上的所有网页。您还可以使用 Sitemap 提供有关您网站的其他信息，如上次更新日期、Sitemap 文件的更新频率等，供搜索引擎参考。

## 一、安装sitemap插件
我的网站也安装了自动生产sitemap的插件，只是不知为什么生成的sitemap的url不是我网站的域名，设置了也无济于事。


```
plugins:
  - jekyll-sitemap

```


## 二、无需插件自动生产sitemap

在根目录中创建sitemap，修改sitemap文件，内容如下，就可以设置或者修改你需要显示的内容或者格式。生成的sitemap文件在_site目录中，提交的时候提交就好。





## 三、在线生产

这个方法不推荐，就是使用第三方网站[sitemaps](https://www.xml-sitemaps.com/)在线生成，如果站内连接多，时间要比较旧，而且要经常更新，不推荐。


推荐阅读：
[如何让博客被收录](https://muitlog.com/2019/11/12/%E5%A6%82%E4%BD%95%E8%AE%A9%E5%8D%9A%E5%AE%A2%E8%A2%AB%E6%94%B6%E5%BD%95.html)