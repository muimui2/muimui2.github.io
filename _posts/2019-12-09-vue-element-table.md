---
title: vue+element table跨行跨列合并
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/element-table-02.png"
key: 2019120902
---

使用table组件过程中，会遇到一个问题，table跨行跨列怎么实现？

首先在html文档中使用element-ui时需要引入相关的SDN:

```

<!-- import CSS -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- import Vue before Element -->
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<!-- import JavaScript -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>

```

下面是原来的table组件样式：

![](/assets/images/blog-images/VUE/element-table-01.png)

##  1.合并列使用arraySpanMethod函数：

该函数可以返回一个包含两个元素的数组，第一个元素代表`rowspan`，实际上就是给td加上`rowspan`属性，第二个元素代表colspan，实际上就是给td加上colspan属性。也可以返回一个键名为`rowspan`和`colspan`的对象，下面来看例子；



![](/assets/images/blog-images/VUE/element-table-02.png)

### 1.1在表格中加入`:span-method="arraySpanMethod"`属性：

```
<template>
    <el-table
            :span-method="arraySpanMethod"
            :data="tableData"
            border
            style="width: 100%">
        <el-table-column
                prop="date"
                label="日期"
                width="180">
        </el-table-column>
        <el-table-column
                prop="name"
                label="姓名"
                width="180">
        </el-table-column>
        <el-table-column
                prop="address"
                label="地址">
        </el-table-column>
    </el-table>
</template>
```


### 1.2在methods中加入arraySpanMethod函数：

```
new Vue({
    el: '#app',
    data: function() {
        return {
            tableData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1517 弄'
            }, {
                date: '2016-05-01',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1519 弄'
            }, {
                date: '2016-05-03',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1516 弄'
            }]
        }
    },
    methods: {
        arraySpanMethod({row, column, rowIndex, columnIndex}) {
            if (rowIndex % 2 === 0) {//判断条件可以设置成你想合并的行的起始位置，本例子是除了标题第一行
                if (columnIndex === 1) {///判断条件可以设置成你想合并的列的起始位置，本例子是第二列开始
                    return [1,2];//合并第一单元格至第二单元格
                } else if (columnIndex === 1) {
                    return [0, 0];
                }
            }
        },
    }
    
})
```


## 2.合并行：objectSpanMethod


![](/assets/images/blog-images/VUE/element-table-03.png)

### 2.1在表格中加入:span-method="objectSpanMethod"属性

```
<template>
    <el-table
            :span-method="objectSpanMethod"
            :data="tableData"
            border
            style="width: 100%">
        <el-table-column
                prop="date"
                label="日期"
                width="180">
        </el-table-column>
        <el-table-column
                prop="name"
                label="姓名"
                width="180">
        </el-table-column>
        <el-table-column
                prop="address"
                label="地址">
        </el-table-column>
    </el-table>
</template>
```

### 2.2在methods中加入objectSpanMethod函数如下代码：

```
objectSpanMethod({ row, column, rowIndex, columnIndex }) {
    if (columnIndex === 1) {//判断条件可以设置成你想合并的列的起始位置，本例子是第二列开始
        if (rowIndex % 2 === 0) {//判断条件可以设置成你想合并的行的起始位置，本例子是除了标题第一行
            return {
                rowspan: 2,
                colspan: 1
            };
        } else {
            return {
                rowspan: 0,
                colspan: 0
            };
        }
    }
}
```

以上是在element中使用table组件合并行，合并列的问题。

推荐阅读：

[vue限制element-ui 表格显示行数](https://muitlog.com/2019/12/05/vue%E9%99%90%E5%88%B6element-ui.html)

[7个VUE前端精美UI框架](https://muitlog.com/2019/12/05/7vue-ui.html)

[vue引入element-ui的流程和注意事项](https://muitlog.com/2019/12/05/vue-element-ui.html)

[VUE自定义指令图文解读](https://muitlog.com/2019/12/04/VUE%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8C%87%E4%BB%A4.html)

[VUE模板语法快速入门教程](https://muitlog.com/2019/12/04/VUE%E6%A8%A1%E6%9D%BF%E8%AF%AD%E6%B3%95.html)