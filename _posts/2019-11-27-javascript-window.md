---
title: JavaScript-window对象常用属性和方法全集
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/frames.webp"
key: 2019112704
---

本章介绍JavaScript中` window`常用的属性和特性，`window`这个关键字是有双重身份的，在浏览器中，表示一个窗口；在JavaScript中，它是全局作用域`Global`的属性。


## 【1】全局作用域

其实window这个关键字是有双重身份的，在浏览器中，表示一个窗口；在JavaScript中，它是全局作用域`Global`的属性。在下面的例子中，定义的是全局变量时，是数据window的属性，所以可以用window访问，如果不是则不能用window访问。那是不是这样定义的全局标量都是window属性？其实不是，全局标量就是全局变量，并不是window属性，只是可以用`window`访问到而已，还是有差别的，比如在一些老版本的浏览器中，就不能用delete操作符删除全局标量，是可以`delete`掉`window`属性的。另外，可以用`window`来查询是否有`window`属性，而全局变量则不能这样检查。

例如：
```
var name = "小新";
function getAge(){
console.log("2"); 
var old = 52; 
} 
window.age = 12;//直接在window定义标量属性
console.log(window.name);//输出全局变量name的值“小新”
console.log(name);//和上面的结果一样，输出全局变量name的值“小新”
console.log(window.getAge());//执行函数，输出2
console.log(window.old);//undefined
console.log(delete window.name);//true 删除变量
var a = b;//抛出错误；
var c = window.age;
var d = window.name;//
console.log(c);//12 查询到window属性
console.log(d);//undefined  name是全局变量不是window属性。

```


## 【2】窗口关系及框架

Window对象并不总是指向最外层，当web中使用框架frame时，window对象就保存框架中，这时候每个框架都有它自己的window属性。因为每个框架都有name属性，所以可以通过name或者id在访问window对象。如果一个html文档中有多个frame框架，还可以通过索引的方式在访问window属性。
除此之外，也可以用top关键字来访问框架，他的作用如同window，为了重复的使用window对象造成凌乱，所以top表示的是最外层window，也就是浏览器窗口。
例如：

```
window.frames("frame1").contentWindow.name//name = 'frame1'的frame
document.getElementById("frame1").contentWindow.name//id = 'frame1'的frame
window.$("#frame1")[0].contentWindow.name//id = 'frame1'的frame
top.frames[0].contentWindow.name //top表示浏览器
```

![](/assets/images/blog-images/JS/frames.webp)

## 【3】窗口位置

那怎么表示窗口（浏览器）在屏幕中的位置？不同的浏览器有不同的表示方式，有的浏览器用screenLeft和screenTop表示窗口的位置，有的浏览器用screenX，和screenY。不同的属性表示的都是同样的意思，就是浏览器距离屏幕左边和上面的距离，以屏幕的左上交为圆心表示的二维距离，就是窗口的位置。
所以在使用时，首先要判断该浏览器用的是screenLeft还是screenX。另外窗口是可以移动的，可以用moveBy和moveTo方法移动，如下面的例子。不过其他教程说这两种方法会被禁用，我试了以下，确实不行，移动不了，然后我用`window.open( )`打开一个新的窗口，在对新的窗口进行移动就可以了。
例如：
```
var x,y;
if(window.screenLeft){// 判断浏览器用的是screenLeft还是screenX
x= window.screenLeft;
y= window.screenTop;
}
else{
x= window.screenX;
y= window.screenY;
}
console.log(x+","+y)//输出0，0


window.moveBy(0,500);
window.moveBy(200,0)//moveBy是在X或者Y上移动；
window.moveTo(500,200);//moveTo是在X,Y上都有移动

```


## 【4】窗口大小
在窗口的大小中，浏览器提供了4个属性，innerWidth，innerHeight和outerWidth，outerHeight。innerWidth是窗口内的可视宽度，也就是页面的宽度；而outerWidth表示的是窗口的宽度。上面都是window的属性，在浏览器中，document.documentElement.clientWidth保存了页面视口的信息，document.body.clientHeight保存了body文档的视口的信息。区分这几个属性运用起来就不难了。
除此之外，可以用resizeTo（）和resizeBy（）来调整窗口的大小，用法和上面window对象中窗口位置移动的方法一样，resizeTo是新的宽度和高度，resizeBy是在原来的尺寸上改动。
例如：
```
var pagex = window.innerWidth;//可视宽度
var winx = window.outerWidth;//窗口宽度
console.log(pagex);
console.log(winx);

var pageW = document.documentElement.clientWidth;//可视宽度
var pageH = document.body.clientHeight;//页面高度
console.log(pageW);
console.log(pageH);

window.resizeTo(500,500);
```
window.resizeBy(500,500);



## 【5】导航及打开新窗口
Window.open( )可以作为导航和打开新的窗口。Window.open( )接受4个参数，第一参数是一个url地址，第二参数是target值，可以是一个框架的名或者是target的属性值_blank等，第三个参数是对新打开的窗口的设置，是一段对窗口特性设置的字符串，第四个窗口是一个布尔值，true表示替换当前窗口，false表示另外打开新的窗口。不过我试了一下，两个值貌似都是打开新的窗口，替换原来的窗口实效？然后我把第二个参数去掉了，结果是在原来的窗口打开了新的连接，不会替换原来的连接，我以为是替换原来页面的连接，原来是我误解了。
例如：
```
<a href="https://www.baidu.com/" target="win">打开新页</a>
window.open('https://www.baidu.com/','win','width:200,height:200,top:100, left:100','false')//和以上作用等同，都是打开新页面
```




### 1、调整窗口

另外，你有没有发现之前提到的窗口移动moveBy和窗口设置大小resizeTo都被浏览器禁止了，所以无效。这两个属性对于新打开的窗口是有效的。
例如：

```
var newwin;
function openwin(){
newwin = window.open('','','width=200,height=100,top=200,left=200');//定义窗口
}
function movewin(){
newwin.moveTo(400,400);//窗口移动
newwin.resizeTo(500,500);//调整窗口大小
}
```


### 2、屏蔽弹窗

现在的浏览器都带有窗口屏蔽程序，避免那些广告弹来弹去，而且浏览器的屏蔽程序并不是把窗口屏蔽，而是把弹窗都放到右下角了，只显示弹窗的标题。
要手动屏蔽其实也简单。
例如：
```
newwin = null;
```


## 【6】间歇性调用与超时调用

间歇性调用与超时调用和超时调用都是window对象的方法。超时我们平时比较常见，setTimeout( )有两个参数，第一个参数是一个包含代码块的字符串，在这里，建议使用函数，因为函数具有整体性，字符串解析起来废内存；第二个参数是一个超时时间，超多该时间，代码块才会被执行。因为JavaScript是一个单线程语言，所以执行代码时会有一个队列，都是等待执行的程序，超时时间就是过了多久之后吧程序加入到队列中，如果队列中没有没有程序在排队，那么setTimeout中的程序会马上执行。否则要等前面的执行了才能执行setTimeout中的程序。更神奇的是，setTimeout方法会返回一直数值，是这个方法在程序中的id,用于表示该程序，可以用这个id作为方法去找到这个超时调用然后用clearTimeout方法停止执行它。

间歇调用其实和超市调用一样的用法，也是带两个参数，不过，间歇调用会隔一段时间就重复调用，所以清除间歇调用尤为重要。而且间歇调用会在上一个间歇调用还没完成时就执行下一个了，所以有点不靠谱，还是老老实实使用setTimeout吧。
例如：
```
var timeoutID = setTimeout(function(){
alert("超时调用")
},1000)//设置1000毫秒向队列添加函数
console.log(timeoutID);//id是1
clearTimeout(timeoutID);//清除setTimeout调用

var IntervalID = setInterval(function(){
alert("超时调用")
},500)//设置1000毫秒向队列添加函数,并且会重复调用
clearInterval(IntervalID);//清除setInterval调用
```


## 【7】系统对话框
系统对话框是window对象的属性，浏览器有三个方法对话框，分别是alert（）,confirm（）和prompt（）。系统对话框是页面没什么关系，也没有css样式和html，是增强了web应用程序的一种便捷方式。alert（）是警告的作用，只是弹窗出来通知，没有其他反馈的信息；而confirm（）多了一个建，分别是确定和取消，确定的时候有进一步的操作，取消则没有；prompt（）方法就更复杂一点了，多了一个输入框，有用户可以输入的信息，返回的是用户输入的结果。在这三种方法执行的时候，程序都是停止的，只有确定或者取消他们的时候，程序才继续执行。
例如：
```
alert("hello");//警告提示


if (confirm("are you sure")){
alert("yes");//按ok的时候
}else{
alert("no")//按取消的时候
}


var name = prompt("what is your name?","");//返回的结果
if(name!=null){
alert(name);
}
```


[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)