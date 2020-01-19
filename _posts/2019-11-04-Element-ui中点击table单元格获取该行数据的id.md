---
title: Element-ui中点击table单元格获取该行数据的id
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: vue element-ui
key: 2019110401
---

## 一、slot-scope="scope" 的理解

slot-scope是作用于插槽，因为在vue中，父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译，父组件的模板是无法使用到子组件模板中的数据，所以vue引入了插槽，实现了父组件调用子组件内部的数据，子组件的数据通过slot-scope属性传递到了父组件



## 二、实例应用

比如我们使用element-ui中的表达，row获取的就是整行的数据，时一个数组。当我想点击某个单元格获取该行数据的id时，我可以这样做：

**html部分：**


```
<template>
  <el-table :data="tableData" stripe border style="width: 100%">
    <el-table-column prop="device_id" label="设备ID"></el-table-column>
			<el-table-column prop="factory_name" label="工厂名称"></el-table-column>
			<el-table-column prop="work_position" label="工位"></el-table-column>
			<el-table-column prop="cur_people_num" label="当前人数">
				<template slot-scope="scope">
					<a @click="showImages(scope.row.id)">{{scope.row.cur_people_num}}</a>
				</template>
			</el-table-column>

  </el-table>
</template>
```


**js部分：**

```
showImages(id){
				console.log(id);
			}
```