---
title: The following paths are ignored by one of your .gitignore filesxxx
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: GIT
key: 2019121703
---

git添加文件提交报错The following paths are ignored by one of your .gitignore files:

xxx的问题解决

 

提交git的时候发现有些文件_site没被git提交，需要手动添加。

代码如下：



```ruby
git add _site

The following paths are ignored by one of your .gitignore files:

_site
```

 

会报错。大概就是说这个文件被忽略了，大概是在哪里忽略了我也不知道，可以用如下命令查：

```ruby
git check-ignore -v _site

.gitignore:188:_site/  _site
```

打开文件，真的看见了，要把_site/ 注释掉，保存。

 

```ruby
# jekyll

Gemfile.lock

package-lock.json

_site/（注释掉）

.sass-cache/

.jekyll-metadata

.jekyll-cache/

```


然后在添加文件提交就可以了。

 

如果想删除远程文件代码如下，具体情况应该会有提示增加一些其他命令。

```ruby
git rm -r _site


```

 