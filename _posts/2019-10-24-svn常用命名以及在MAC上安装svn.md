---
title: svn常用命名以及在MAC上安装svn
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: svn
cover: "/assets/images/blog-images/SVN/svn界面图.webp"
key: 2019102401
---

除了用git上传到远程仓库之外，还可以用svn。我之前用的是window系统，所以可以安装小乌龟，可是现在公司配了苹果电脑，发现没有小乌龟的ios版本，所以只能被迫用了大半个月的svn命令。这个使用命令在一开始的时候很不习惯，因为它不能一次性add 提交，只能add 一个指定的文件或者问价类型。所以如果一下子改了很多文件的话，就不是很方便。（如果你看到最后就有安利哦）



下面是svn常用的命令：


**一、检出代码**


命令：
`svn co `
是svn checkout 的缩写，后面可以更上地址。




**二、添加到本地临时仓库**


进入到需要添加的文件的目录
命令：
`SVN add .`
添加所有带html后缀的文件：svn add .*html
重点来了，如果你不想这么麻烦一个个文件添加，那么下面这行命令很适合你：
`SVN add . --no-ignore --force`




**三、查看状态**


这个和git相似：
`svn status`




**四、提交代码**


命令：这个也是和git相似。
`SVN commit -m ‘命名’ `
可以缩写为 svn ci





**五、更新**


命令：
`SVN up`
是svn update 的意思。



**
六、svn命令提交到指定的路径**


如果路径更变，比如我们拿别的项目来修改，路径变了，需要重新提交到指定的位置。
命令：
`SVN import 本地路劲 远程指定路径 -m ‘说明’`




**七、mac 上安装svn 软件 SniilSVNLite**


经过上面的曲折，终于来到了这里。因为上面的命令很限制，用惯小乌龟的都知道会有一个小标志，那些文件提交了那些有变动了需要提交，都会有提示，包括冲突的解决，所以，我还是决定去搜一下，结果一搜，直接在app store 就可以下载安装使用。界面非常简洁，配置很简单。

![](/assets/images/blog-images/SVN/svn界面图.webp)

![](/assets/images/blog-images/SVN/SVN操作图.webp)


应有尽有，不要为了上存的命令把自己搞死了，重点还是放在项目上吧。
忘记今天是1024了，祝程序员快乐，祝我自己快乐。