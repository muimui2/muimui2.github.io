---
title: 运行gulp错误gulp[22202]src node_contextify.cc 626 static void
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: GIT
key: 2019101601
---

我们从GitHub上把web app克隆下来之后，要在本地真机查看，也要编译一次代码，这时要用到gulp命令行，可是当运行gulp出现以下的错时可以采用以下的方式解决。前提时安装node.js和安装了项目依赖（npm install）。

在项目运行gulp时会出现一个错误：错误的原因可能是升级node出现的错处。

```
gulp[22202]: ../src/node_contextify.cc:626:static void node::contextify::ContextifyScript::New(const FunctionCallbackInfo<v8::Value> &): Assertion `args[1]->IsString()' failed.
```


解决办法：

第一步：安装natives
意思是使用Node.js的本机JavaScript模块。
`npm install natives`


第二步：清除有问题的依赖
先删除依赖，清除因为版本问题的node_modules文件夹。
rm -r node_modules


第三步：重新安装
再重新安装项目依赖，意思是使用npm install将按照package.json安装所需要的组件放在生成的node_modules文件夹中。
`npm install `