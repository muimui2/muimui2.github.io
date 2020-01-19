---
title: vue element-UI实现分页查询
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue
cover: "/assets/images/blog-images/VUE/vue分页完成-02.webp"
key: 2019120102
---

在做项目的过程中，查询数据是最基本不够的了，在使用element-ui框架的基础上，如何使用vue.js进行分页查询？
下面是我的用例和说明：

![](/assets/images/blog-images/VUE/vue分页-01.webp)

## Html部分：

以下的表格中的属性data的算法是运用了`slice（）`方法返回的是一个数组。就是要限制每页显示的行数。

```
<div id="example">
<template>
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

<el-pagination background 
layout="prev, pager, next, sizes, total, jumper"
:page-sizes="[5, 10, 15, 20]"//每页展示条选择组件
:page-size="pagesize"//每页展示条
:total="tableData.length"
@current-change="handleCurrentChange" // currentPage改变时会触发
@size-change="handleSizeChange" //pagesize改变时触发
>
</el-pagination>
</template>
</div>
```



## Vue.js部分：

pagesize属性是设置每页显示的行数，currentPage是当前页数，初始化是1，就是第一页的意思。

```
<script>
new Vue({
el: '#example',
data() {
return {
 pagesize: 5,
currentPage:1,
tableData: [...
],// 数组

}
},
methods: {
                handleCurrentChange(cpage) {
                    this.currentPage = cpage;
                },
                handleSizeChange(psize) {
                    this.pagesize = psize;
                },
},
})
</script>
```


![](/assets/images/blog-images/VUE/vue分页完成-02.webp)


以上是例子，在具体项目中，数据都是请求返回的，所以一下是具体的项目事例：



不同担心，在js文件中加入连接：

```
  <script type="text/javascript">
    Vue.use(ELEMENT)
axios.defaults.baseURL = '数据路径'
  </script>


//然后再vue中再初始化数组list[ ].
new Vue({
      el: '#app',
      data: {
        list: [],
        pagesize: 10,
        currpage: 1
      })
```


最后别忘记了把表格上面的数组替换成你定义的数组的名称。

```
<el-table :data="list.slice((currpage - 1) * pagesize, currpage * pagesize)"
</el-table>
```


推荐更多阅读：

[v-if条件语句和v-for循环语句简明教程](https://muitlog.com/2019/11/25/v-if%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5%E5%92%8Cv-for%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B.html)


[vue router-link属性集合详解](https://muitlog.com/2019/11/26/vue-router-link.html)


[vue如何创建路由vue-router](https://muitlog.com/2019/11/27/vuevue-router.html)


[vue之计算属性和监听属性——快速入门](https://muitlog.com/2019/11/27/vue%E4%B9%8B%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E5%92%8C%E7%9B%91%E5%90%AC%E5%B1%9E%E6%80%A7.html)