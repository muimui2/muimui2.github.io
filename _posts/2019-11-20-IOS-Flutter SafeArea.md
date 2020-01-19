---
title: IOS 异形屏幕适配——Flutter SafeArea
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: H5 IOS 问答题
cover: "/assets/images/blog-images/other/iOS适配异性屏幕.webp"
key: 2019112003
---

今天在用H5开发app的过程中，我遇到了一个问题，就是在测试的时候发现iPhoneX以上的手机下面会有一道白色的局域，查了一下，是安全局域 SafeArea。为了让app适配iPhoneX以上的屏幕，我找到了[Flutter](https://flutter.dev/)。

![](/assets/images/blog-images/other/iOS适配异性屏幕.webp)

## 提出问题

问题：
![](/assets/images/blog-images/other/ios底部图片.webp)


我想要的效果：
![](/assets/images/blog-images/other/ios底部图片2.webp)


我看了教程，是在头部添加如下代码：

`<meta name="viewport" content="viewport-fit=cover" />`


可是并没有什么作用。



## 解决办法

于是我看到了 flutter ，项目安装 install flutter（安装看官方文档）。

Flutter 引入了 SafeArea（安全区域），我们只需要在代码中加入SafeArea

```
 Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: SafeArea(  // 加入SafeArea
        child: ListView.builder(itemBuilder: (context, index) {
          return Padding(
            padding: EdgeInsets.only(left: 10, bottom: 18),
            child: Text(
              'Data',
              style: TextStyle(fontSize: 18),
            ),
          );
        }),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
	
```
	
	

	还可以特定指定位置：

	
```
SafeArea(
top: false,
bottom: true,
left: true,
right: false,
),
```