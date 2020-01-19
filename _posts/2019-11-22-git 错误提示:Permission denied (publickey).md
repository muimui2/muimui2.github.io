---
title: git 错误提示:Permission denied (publickey)
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: GIT 问答题
key: 2019112201
---

最近把项目部署到 [coding](https://coding.net/)。因为之前已经添加过git ssh公钥，然后使用coding的时候再添加了一次，所以会出现git不知道用哪个公钥的情况，二不是没有添加。当然如果你还没添加，也会是找不到的，我说的这种情况是已经添加了的。

解决办法：
ssh-add命令是把专用密钥添加到ssh-agent的高速缓存中。


## 一、ssh-add语法
```

ssh-add [-cDdLlXx] [-t life] [file ...]

```


## 二、ssh-add操作选项

```
-D：删除ssh-agent中的所有密钥.
-d：从ssh-agent中的删除密钥
-e pkcs11：删除PKCS#11共享库pkcs1提供的钥匙。
-s pkcs11：添加PKCS#11共享库pkcs1提供的钥匙。
-L：显示ssh-agent中的公钥
-l：显示ssh-agent中的密钥
-t life：对加载的密钥设置超时时间，超时ssh-agent将自动卸载密钥
-X：对ssh-agent进行解锁
-x：对ssh-agent进行加锁
```



## 三、实例

把专用密钥添加到 ssh-agent 的高速缓存中：

```
ssh-add ~/.ssh/id_dsa（公钥名称，默认id_dsa）

//删除公钥
ssh-add -d ~/.ssh/id_xxx.pub
```