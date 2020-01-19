---
title: JavaScript中级教程—— JavaScript 数组操作总结
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
key: 2019121903
cover: /assets/images/blog-images/JS/JavaScript封面.webp
---

其实在JavaScript中最重要的是方法函数的运用和数组的处理。在面试题中肯定会问到数组的处理，包括数组的排序和转换。所以本章就来总结一下数组的方法和特性。

## 一、Array长度

可以通过length属性获得Array的长度，同时也可以改变Array的长度。
例如：

```ruby
var arr=[1,2,3.14,'12','？']
console.log(arr.length)//5
arr.length = 8;
console.log(arr)
console.log(arr[6])

```

## 二、查找和修改元素

上面已经说过可以通过索引在找到元素，反过来也可以通过索引来改变元素。
例如：
```ruby
console.log(arr[2])
arr[2] = 3;
console.log(arr)

另外还可以用过索引来改变数组的长度。
例如：
var arr1 = ['a','b','c','d'];
console.log(arr1.length)
arr1[5] = 'e';
console.log(arr1)
console.log(arr1.length)
```


## 三、indexOf指定元素位置

数组可以通过indexOf()方法来搜索指定元素在数组中的位置，也就是查找索引是多少。
例如：
```ruby
var arr2=[1,2,3,'a','b']
console.log(arr2.indexOf('a'))//3
```


## 四、slice 截取数组

`Slice(start,end)`方法就像substr等截取字符串长度的方法一样，只不过slice只用于数组，返回一个新的Array。`Slice()`包含两个可选参数，第一个是截取数组的开始位置，第二个参数结束位置，截取的数组元素不包含第二个参数。
例如：
```ruby
var arr3 = ['a','b',1,2,3]
console.log(arr3.slice(0,2))//["a", "b"]
```
如果不传参数会怎么样？利用Slice的这一特性，可以复制一个新的数组。
例如：

```ruby
var arr4 = arr3.slice()
console.log(arr4)//["a", "b", 1, 2, 3]
```
## 五、数组元素的添加和删除

对数据的操作，无非就是添加修改和删除。

### 【1】push和pop

`push()`是从Array的末尾添加元素，而pop是把Array的最后一个元素删除，返回所删除的元素。
例如：
```ruby
var arr = ['a','b','c',1,2,3];
arr.push(4);
console.log(arr);
arr.pop();
console.log(arr)

```

### 【2】unshift和shift

Unshift和push的用法相同，作用刚好相反。Unshift是在数组的前面对数组进行添加和使用shift在数组的前面对数组进行删除的方法。

例如：
```ruby
var arr = ['a','b','c',1,2,3];
arr.unshift('121212');
console.log(arr);
arr.shift();
console.log(arr)

```

### 【3】splice

`splice()`方法向/从数组中添加/删除项目，然后返回被删除的项目。Splice()方法是既不是从前面操作数组也不是从后面操作数组，而是可以指定一个位置，从该位置开始删除指定的元素个数，然后再从该位置增加若干元素。
语法：
```ruby
arrayObject.splice(index,howmany,item1,.....,itemX)
```
例如：
```ruby
var arr1 = [1,2,3,4,'a','b','c'];
console.log(arr1.splice(0,4,'12','34'))//[1, 2, 3, 4]
console.log(arr1);// ["12", "34", "a", "b", "c"]
```
Splice也可以是只删除不增加，只需要写前面两个参数。

## 六、数组的排序

JavaScript对数组的操作排列包括顺序和倒序。

### 【1】顺序

数组是一个集合，一推无序的元素。所以可以使用sort()对数组进行排序，直接调用时，按照默认顺序排序。
例如：sort
```ruby
var arr = ['b','a','c','e','d'];
var arr1 = [1,3,4,2,8,6,7]
var arr2 = ['b','a','c',1,3,4,2,8,6,7,'e','d']
console.log(arr.sort())// ["a", "b", "c", "d", "e"]
console.log(arr1.sort())//[1, 2, 3, 4, 6, 7, 8]
console.log(arr2.sort())//[1, 2, 3, 4, 6, 7, 8, "a", "b", "c", "d", "e"]
```

### 【2】倒叙reverse

`Reverse()`方法和`sort()`方法对立，倒叙。
例如：
```ruby
console.log(arr.reverse())// ["e", "d", "c", "b", "a"]
console.log(arr1.reverse())//[8, 7, 6, 4, 3, 2, 1]
console.log(arr2.reverse())//["e", "d", "c", "b", "a", 8, 7, 6, 4, 3, 2, 1]
```

## 七、连接数组


### 【1】数组连接concat

字符串之间可以用【+】或者反引号	【`...`】连接，那数组呢？用什么方法连接两个数组？

数组之间的连接方法用concat()，其实它是破坏数组，把一个数组拆开，然后然后接收其他的数组或者元素，在返回一个新的数组。Concat()里面的参数就是所插入的元素。

例如：
```ruby
var arr = ['b','a','c','e','d'];
var arr1 = [1,3,4,2,8,6,7]
arr.concat(arr1)
console.log(arr.concat(arr1))//["b", "a", "c", "e", "d", 1, 3, 4, 2, 8, 6, 7]
```

### 【2】字符连接join

join()方法是一个使用在数组元素中的方法，连接数组元素，join()所带的参数就是连接元素的连接符。返回的是一个字符串。如果数组内的元素不是字符串类型的，join()会自动把它变成字符串类型的再进行连接。
例如：
```ruby
var arr = [1,3,4,2,8,6,7];

console.log(arr.join(1));//1131412181617
console.log(typeof(arr.join(1)));//string

console.log(arr.join('-'));//1-3-4-2-8-6-7
console.log(typeof(arr.join('-')));//string

```

## 八、多维数组

多维数组比较好理解，就是数组的某个或者多个元素是一个数组，数组中的数组，就是多维数组。
方法都是一样的，把数组里面的数组当作整体来处理就是简单了很多。访问多维数组中的元素一样也是通过索引。
例如：
```ruby
var arr = [1,2,[3,4,5,],[6,7],['8','9']];
console.log(arr);//[1, 2, Array(3), Array(2), Array(2)]
console.log(arr[2][1]);//4

```

推荐阅读：

[JavaScript初级教程——引入方式及调试方法](https://muitlog.com/2019/12/18/javascript-引入方式及调试方法.html)

[JavaScript初级教程——基本语法和注意事项](https://muitlog.com/2019/12/18/javascript-基本语法和注意事项.html)

[10道JavaScript面试题——画重点](https://muitlog.com/2019/12/12/10javascript.html)
[JavaScript数据类型——前端入门](https://muitlog.com/2019/12/11/JavaScript%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.html)
[JavaScript对象方法及this用法详解](https://muitlog.com/2019/12/10/javascript-this.html)







