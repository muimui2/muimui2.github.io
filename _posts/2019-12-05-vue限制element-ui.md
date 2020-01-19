---
title: vue限制element-ui 表格显示行数
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/element限制行数.png"
key: 2019120503
---

如何限制VUE项目中，element-UI的显示行？想控制每页的显示的行数怎么控制的？

![](/assets/images/blog-images/VUE/element限制行数.png)

解决办法：

使用`slice()`方法，`slice() `方法可从已有的数组中返回选定的元素。返回的数据是数组。

`tableData`是数据组,
`Pagesize`是限制每页的行数，
`currentPage`是第几页数


```
<el-table
:data="tableData.slice((currentPage-1)*pagesize,currentPage*pagesize)"
style="width: 100%"
>
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

data() {
return {
pagesize: 5,
currentPage:1,
}
})
```


推荐阅读：
[VUE模板语法快速入门教程](https://muitlog.com/2019/12/04/VUE%E6%A8%A1%E6%9D%BF%E8%AF%AD%E6%B3%95.html)


[VUE自定义指令图文解读](https://muitlog.com/2019/12/04/VUE%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8C%87%E4%BB%A4.html)


[vue element-UI实现分页查询](https://muitlog.com/2019/12/01/vue-element-ui.html)

[vue之Mixins混入结合图例易理解](https://muitlog.com/2019/11/29/vue-mixins.html)


[前端引入模板的4种方法](https://muitlog.com/2019/11/27/%E5%89%8D%E7%AB%AF%E5%BC%95%E5%85%A5%E6%A8%A1%E6%9D%BF%E7%9A%844%E7%A7%8D%E6%96%B9%E6%B3%95.html)