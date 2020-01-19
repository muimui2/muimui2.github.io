---
title: JavaScript引用类型及使用方法详细说明
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/JavaScript封面.webp"
key: 2019111603
---

本章我们来学习JavaScript中的引用类型的使用方法。

引用类型是一种数据类型，把数据和功能组织在一起。引用类型又被称为对象定义，因为它们描述的是一类对象所具有的方法和属性。因为在JS中不具有类的概念。

![](/assets/images/blog-images/JS/JavaScript封面.webp)

## 一．Object类型

创建Object实例有两种方式，第一种是使用new操作符，第二种是对象字面量的方式。

### 1、new操作符表达法

例如：

```
var person = new object();
person.name = "Luara";
person.age = 25;
```



### 2、字面量表达法

使用字面量的表达方式目的是简化创建包含大量属性的对象的过程，而且使用 { } 花括号概括起来， 让人有一种代码被封装起来了的感觉。所以程序员还是比较喜欢使用这种方式。

例如：
```
var person = {
name:"Luara",
age:25
}
```




## 二、Array 类型

如同上面的方法一样，可以用new创建一个数组实例，不过在JS中，数组比较特别，可以省略new创建实例，更加奇怪的是，如果在带着一个值创建数组过程中，如果该值是数字，就是Number类型的，则表示创建的数组长度为1，只有这一个值；出了Number类型的其他类型，都统一表示为创建了一个包含该数值的数组，而不是只有一个值。
另外，对于数组的长度length属性，它不只是单纯的只读数组的长度，也是可以设置的。

例如：

```
var color = new Array(3); // 使用new操作符创建一个数组只有3的数组，和下面等价
var color = Array(); // 省略
var names = Array("Greg"); // 创建一个包含 1 项，即字符串"Greg"的数组
var arr = ["red", "blue", "green"];
arr.length = 1;
console.log(arr[2]) // undefined 改变了数组长度，访问不了索引为2的元素
```




### 1、栈方法

ECMAScript提供了一种栈方法，可以让数组的行为类似于其他结构，栈方法的特点是【后入先出】，就像堆罗汉那样，最后进来的会排在最上面，当要出去的时候，就是刚刚最后进来的先出去。在数组里面，这里的“进来”和“出去”就是对数组进行的操作添加元素和删除元素。

```
var arr = ["red", "blue", "green"];
arr.push("black");
console.log(arr[3]) // black 添加进来的在数组的最后排列
var item = arr.pop()
console.log(item) // black 返回最后一个删除的元素
```



### 2、队列方法

队列方法的原则也是【后入先出】，不过不同的是，是从数组的前端操作数组，有两个方法shift（）方法和unshift（）方法。shift（）是取得第一项，unshift（）方法是返回新数组的长度。

例如：

```
var arr = ["red", "blue", "green"];
arr.push("black");
console.log(arr[3]) // black 添加进来的在数组的最后排列
var item = arr.pop()
console.log(item) // black 返回最后一个删除的元素
console.log(arr.shift()) // red 返回第一个项
console.log(arr.unshift()) // 返回新数组的长度2
```


### 3、重排序方法

对于数组的操作，重排序的方法有两种，reverse()和 sort()。reverse（）是将数组反转过来，sort（）把数组按升序排序，不过要注意的是，sort（）方法会调用每个数组项的toString（）转型方法，所以如果是排序数值的数组，进过toString（）转型，会变成比较字符串的大小而排序。所以想要数值升序排列，需要写一个函数来比较数值的大小从而排序，这样的话不仅可以排序升序，也可以设置降序。

例如：

```
var num = [1,2,3,5,12];
var re = num.reverse();
var so = num.sort();
console.log(typeof(re)); // object 返回一个object类型
console.log(typeof(so)); // object
console.log(so) // [1, 12, 2, 3, 5] 会想执行toString（），比较的实际是字符串

// 比较数值大小的函数，从而使得数字的排序是按照数值的大小，而不是按照字符串的大小
function compare(val1,val2){
if(val1 < val2){ // 如果第一个数比第二个数小，返回-1，如果想要降序的，返回1就可以了，下面也同理。
return -1;
}
else if(val1 > val2){ // 如果第二个数比第一个数小，返回1
return 1;
}
else{
return 0; // 如果两个值相等，返回0
}
}
console.log(num.sort(compare)) // [1, 2, 3, 5, 12] 
// 排序的时候带上比较数值大小的
```




### 4、操作方法

对数组的操作方法就是删除，插入和替换，在这里首先要介绍两种方法，concan( )方法和slice( )方法，他们对于数组的操作不是对原来数组的操作，是对数组的副本，也就是会复制多一个副本出来，不是在原来的数组上进行的操作。
concan( )是对数组的增加，携带的参数就是想要增添到副本数组里面的数值或者是数组，返回的是一个新的数组。slice( )可以理解为截取数组的长度、，操作的也是数组的副本，返回一个截取后的数组。
不过另外，JS还有一个更加厉害的操作数组的方法，那就是splice（）方法，不单只可以插入元素，还可以删除和替换，这里的替换实际就是同步的插入和删除，根据携带的参数不同，表达的意思不同，我们需要注意。

例如：

```
var color = ["red", "blue", "green"];
// 带两个参数是，第一个参数是位置，第二个参数是项数，表示的是删除
var removed = color.splice(0,1);
console.log(color); // ["blue", "green"]
console.log(removed); // ["red"] 返回的是数组

// 带三个以上的参数并且第二个参数是0，表示的是插入，第一个参数是位置，第二个参数是移除的未知，第三个参数之后的都是要插入的项
var add = color.splice(1,0,"yellow","orange");
console.log(color); // ["blue", "yellow", "orange", "green"]
console.log(add) // 返回的是一个空数组
var replace_removed = color.splice(1,1,"yellow","orange");
console.log(color); // ["blue", "yellow", "orange", "orange", "green"]
console.log(replace_removed); // ["yellow"] 返回删除的项
```



### 5、迭代方法

在JS中有5中迭代数组的方法分别是，every(),some(),forEach(),map(),filter()他们都可以接收两个参数，第一参数可以是在每一项上运行的函数，第二个参数是该函数运行的作用域（影响this的值），这里的参数函数带三个参数，第一个参数是数组元素的项，第二个参数是元素的位置，第三个参数是该数组。
every（）和some（）相似，就像逻辑运算符的&& || 那样，every（）要求数组内的全部元素都是true才返回true。而some（）只要数组内的一项是true那就会返回true。forEach（）和for()相似。
需要一提的是，filter（）这个方法对于数据的筛选大有作用。

```
var numbers = [1,2,3,4,5,4,3,2,1];
var eveResult = numbers.every(function(item,index,array){
return (item > 2)
});
var filterResult = numbers.filter(function(item,index,array){
return (item > 2)
});
var mapResult = numbers.map(function(item,index,array){
return (item * 2)
});
console.log(eveResult) // false 并不是每一项都大于2
console.log(filterResult) // [3, 4, 5, 4, 3] 返回的是数组
console.log(mapResult) // [2, 4, 6, 8, 10, 8, 6, 4, 2] 返回的是一个数组
```




### 6、递归方法

JS中有两个归并数组的方法——递归方法。它们分别是reduce( )方法和reduceRight（）方法。这两个方法都会迭代数组中的所有项，然后构建一个最终的返回值。很显然，reduce（）方法会从数组的第一项开始，到数组的最后，reduceRight（）会从数组的最后一项开始，迭代到数组的第一项。这两个方法中的函数接受四个参数，前一个值、当前值、项的索引和数组对象。

例如：

```
var numbers = [1,2,3,4,5,4,3,2,1];
var val = numbers.reduce(function(one,two,index,array){
return one + two;
})
console.log(val) // 25 1+2+3+...+1
```



## 三、Date类型

我们在创建一个日期对象，使用new操作符和Date构造函数就可以了。

例如：

`var now = new Date();`


Date.parse( )方法可以把日期格式转换成字符串格式。不过在new Date("May 25, 2004")时构造函数时，也会在后台调用Date( )，所以直接把字符串写在Date( )函数里面作为参数就可以了。
另外，在JS中添加了Date.now( )的方法，就是捕获当前的时间，返回的是时间截。

例如：

```
var times = new Date();
var time = new Date("May 25, 2004");
console.log(time) // Tue May 25 2004 00:00:00 GMT+0800 (中国标准时间)
console.log(typeof time) // object 把时间格式的字符串转为日期对象。
var now = Date.now();
console.log(now) // 1563376147322 时间截
var start = +new Date(); // 创建
var end = +new Date();
console.log(end - start) // 0毫秒
```





## 四、RegExp类型

JS通过RegExp类型在支持正则表达式。每个正则表达式带有一个或者多个标签，这些标签标明表达式的行为。下面有三个标志：

* g：表示的是全局模式（global），该模式被应用于所有字符串，一旦发现有匹配的马上停止。
* i：表示不区分大小写模式（case-insensitive），即在确定匹配项时忽略模式与字符串的大小写；
* m：表示多行模式（multiline），即搜索到行的末尾时如果还没找到需要匹配的目标，还会继续向下一行搜索。

```


/* 
* 匹配字符串中所有"at"的实例
*/ 
var pattern1 = /at/g; 
/* 
* 匹配第一个"bat"或"cat"，不区分大小写
*/ 
var pattern2 = /[bc]at/i; 
/* 
* 匹配所有以"at"结尾的 3 个字符的组合，不区分大小写
*/ 
var pattern3 = /.at/gi;
```





## 五、Function类型

我们要理解的是，函数时一个对象，函数名是指针。要访问函数指针只需要去掉后面的括号就可以了。一个函数可以有多个函数名。所以函数是没有重载的。怎么理解重载？就是定义了两个同名的函数，然而这两个函数并不能合并起来，最后定义的那个函数会代替第一次定义的。
另外函数声明和函数表达式的区别，在执行代码过程中，JS引擎会先读取函数声明，在遇到需要执行函数的方法是，才会执行函数表达式。而且JS会吧函数声明提前，这样，就算函数的执行方法在定义函数之前书写也是可以的。
但是，如果是函数表达式（定义的是匿名函数，然后把函数表达式赋值给变量），执行函数的方法在表达式之前是不可行的。

例如：

```
function addnum(num){
return num + 100;
}
function addnum(num){
return num + 200;
}
console.log(addnum(100)) // 300 这里的addnum是第二个函数
```



### 1、函数内部属性

在函数内部，有两个特殊的对象：arguments 和 this。arguments 是一个类似数组的对象，是参数的集合，arguments 有一个属性是callee，这个属性是一个指针，指向拥有arguments 对象的函数，也就是指回这个函数。因为我们上面提到函数可以同名，函数名其实就是一个指向函数对象的指针，所以函数本身其实和函数名的关系并不大，只能作为一个函数的标识。所以当我们在一个函数内部使用函数自己本身时，还使用函数名就不是很恰当。
对于this就是作用域上的问题，如果在全局中的函数内调用this则相当于window。是在对象的方法中，this代表的是对象的属性。

例如：
```

function factorial(num){ 
if (num <=1) { 
return 1; 
} else { 
return num * factorial(num-1) 
} 
}
console.log(factorial(4)) // 4*3*2=24
// 以上函数代码可以写成如下更好
function factorial(num){ 
if (num <=1) { 
return 1; 
} else { 
return num * arguments.callee(num-1) 
} 
}
```



### 2、函数的属性和方法

因为函数也是对象，所以函数具有属性和方法。每个函数都包含两个属性：length 和 prototype。其中length 表示接受函数参数的个数，也就是arguments的长度。而prototype属性就是保存实例方法的真是存在，比如toString( )和 valueOf( )等方法实际上都保存在 prototype 名下。
每个函数都包含两个非继承而来的方法：apply()和 call()。这两个函数的作用实际上等于设置函数体内this对象的值。这两个方法的不同之处在于接受参数的方式不同，apply()方法接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是 Array 的实例，也可以是arguments 对象。对于 call()方法而言，第一个参数是 this 值没有变化，变化的是其余参数都直接传递给函数。换句话说，在使用call()方法时，传递给函数的参数必须逐个列举出来。
例如：

```
function sum(num1, num2){
return num1 + num2;
}
function callSum(num1, num2){
return sum.call(this,num1, num2 )
}
function callSum1(num1, num2){
return sum.apply(this, [num1, num2]);
}
console.log(callSum(15,10)) // 25
console.log(callSum1(20,10)) // 30 

```





## 六、基本包装类型

出了引用类型之外，还有基本类型，不过为了便于操作基本类型的值，所以JS提供了三种特殊的引用类型，Boolean、Number 和String。他们和上面Object类型相似，不过也具有基本类型的行为。为什么具有和引用类型相似的性质呢？因为当读取一个基本类型值得时候，后台会自动创建相应的基本类型包装对象，便于我们调用一些方法来操作数据。
但是，我们不能新建对象的属性或者方法，因为这些自动创建的基本类型包装方法会在执行之后就销毁，所以是访问不到创建的属性和方法的，除非我们用new来创建实例。

例如：

```
var ss = "some text"; // 会自动创建实例，也就是基本包装类型
ss.color = "red"; // 新建属性 不过在执行完之后就会销毁
console.log(ss.color) // undefined

var s1 = new String("some text"); // 创建实例 typeof 会返回"object"
var s2 = s1.substring(2); // 调用方法substring
s1.color = "red" // 创建属性
console.log(s1.color ) // red访问属性
```




## 七、单体内置对象

什么是单体内置对象，就是不依赖于人格宿主环境对象，这些对象在程序执行之前就已经存在了，就已经实例化了，比如Object、Array 和 String。另外，还定义了两个单体内置对象：Global 和 Math。


### 1、Global 对象

所有在全局作用域中定义的属性和函数，都是Global 对象的属性。
Global 对象有两个方法可以对URL进行编码以发送给服务器，这两个方法分别是encodeURI()和 encodeURIComponent()方法，encodeURI()不会对原来的字符进行编码，只会对空格进行编码，就是除了空格之外其他字符都原封不动。而encodeURIComponent()则会对任何非标准字符进行编码。所以在实际应用中，使用encodeURIComponent()比encodeURI()的情况要多。既然有了编码， 那就需要有解析编码的反编码，分别是decodeURI()和decodeURIComponent()方法。但是需要主要的是，他们解析的URL字符串只是被encodeURI()和 encodeURIComponent()方法编码过后的字符串，对于其他编码他们是不会解析的。

例如：

```
var urls = "D:/xm/example/javascript-14.html";
var encode = encodeURI(urls); // 编码字符串，除了空格之外其他都不会有变化
var encodeCom = encodeURIComponent(urls); // 任何非标准的都会被编译
var deco = decodeURI(encode); // 解析经过encodeURI编码的字符串
var decoCom = decodeURIComponent(encodeCom); // 解析经过encodeURIComponent编码的字符串
console.log(encode); // D:/xm/example/javascript-14.html
console.log(encodeCom); // D%3A%2Fxm%2Fexample%2Fjavascript-14.html
console.log(deco); // D:/xm/example/javascript-14.html
console.log(decoCom); // D:/xm/example/javascript-14.html
```



### 2、Math对象

Math对象包含的属性和方法大多都是数学计算会用到的特殊值或者方法。比如求最大值和最小值的时候可以使用 min()和 max()方法，这两个方法可以从所带的参数中筛选出最大值或者最小值，即使参数是字符串类型的数值，也会先通过Number（）转换成Number类型的在进行比较输出。
另外，还可以通过Math.ceil()、Math.floor()和 Math.round()。三个方法得出数值的取舍，Math.ceil()方法是向上舍入，就是无论小数点如何，得出的整数都会比原来的数大；Math.floor()得出的整数都会比原来的数小；Math.round()就是四色五入的规则。
另外还有随机数，random（），指的是0-1之间的随机数。

例如：

```
console.log(Math.max("1",'2',3,'4')); // 先转换成Number类型的，在进行比较
console.log(Math.ceil(10.2)); // 11 向上舍入
console.log(Math.ceil(10.8)); // 11
console.log(Math.floor(10.2)); // 10 向下舍入
console.log(Math.floor(10.8)); // 10
console.log(Math.round(10.2)); // 10 // 四舍五入
console.log(Math.round(10.8)); // 11
console.log(Math.random())
```