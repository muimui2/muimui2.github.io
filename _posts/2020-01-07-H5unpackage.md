---
title: H5中的unpackage文件以及配置文件config
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: H5
key: 2020010701
cover: /assets/images/blog-images/other/weixin.png
---


两天没发布文章文章就觉得个了很久一样，浑身不舒服。
今天来讲下H5地下的unpackage文件夹是干什么用的，以及unpackage>scripts>config.js文件的格式和作用。

## 一、unpackage的作用

1、unpackage是使用uni-app创建项目的时候自带的一个文件，用uni-app创建的app可以在真机测试，在创建项目的时候，会自带一个unpackage文件，在HBuilderX工具栏，点击发行，选择网站-H5手机版，如下图，点击即可生成 H5 的相关资源文件，保存于 unpackage 目录。

2、也可以在微信开发者工具中生成适用于微信平台的代码，在HBuilderX中顶部菜单依次点击 "发行" => "小程序-微信"，输入小程序名称和appid点击发行即可在 unpackage/dist/build/mp-weixin 生成微信小程序项目代码。

![img](/assets/images/blog-images/other/weixin.png)

3、另外，看名字就知道，unpackage是不被打包进项目里面的，不过它协助编译打包，所以要在unpackage下运行gulp打包。
不过打包的文件会存放在其中，这个存放的具体路径可以在manifest.json 中设置。



## 二、unpackage下的config.js文件配置

在unpackage下运行gulp打包之后，会在src中的文件目录中生成main.js，也就是我们项目中的配置问价。是配置app_key和厂商ID这些。因为每个app都是独立的，所以开发app是需要app_key的，app连接产品型号这些要厂商ID。

例如：


```javascript
/*APP 配置参数*/
var isTestApi = false; // 测试服务器
var isLogPrint = true; // 正式服务器
var isLogWrite = false;
/*APP 静态参数*/
var COMPANY_ID = "xxxx"; // 厂商ID
var COMPANY_BRUSH = "xxxx"; 
var APP_KEY_DEBUG = "xxxx"; //测试服务器
var APP_KEY_RELEASE = "xxxx"; 
var APP_SECRET_DEBUG = "xxxx";
var APP_SECRET_RELEASE = "xxxx";


//其他是一些方法
function getAppkey() {
	return isTestApi ? APP_KEY_DEBUG : APP_KEY_RELEASE;
}

function config_isTestApi() {
	return isTestApi;
}

function getAppSecret() {
	return isTestApi ? APP_SECRET_DEBUG : APP_SECRET_RELEASE;
}

function getCompanyId() {
	return COMPANY_ID;
}

function getCompanyIdBrush() {
	return COMPANY_BRUSH;
}


function getHttpDomain() {
	return isTestApi ? "xxxxxx" : "xxxxxxxxx"; // 服务器地址
}

function getWebSocketDomain() {
	return isTestApi ? "xxxxxxxx" : "xxxxxxxx"; 
}

```







