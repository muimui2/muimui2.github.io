---
title: JavaScript面向对象编程及原型链理解【重点】
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: JavaScript
cover: "/assets/images/blog-images/JS/构造函数和对象.webp"
key: 2019120302
---

> 在计算机科学中，对象（英语：object），台湾译作物件，是一个存储器地址，其中拥有值，这个地址可能有标识符指向此处。对象可以是一个变量，一个数据结构，或是一个函数。是面向对象（Object Oriented）中的术语，既表示客观世界问题空间（Namespace）中的某个具体的事物，又表示软件系统解空间中的基本元素。
> 
> 在软件系统中，对象具有唯一的标识符，对象包括属性（Properties）和方法（Methods），属性就是需要记忆的信息，方法就是对象能够提供的服务。在面向对象（Object Oriented）的软件中，对象（Object）是某一个类（Class）的实例（Instance）。
> 
> ——维基百科


## 一、对象是什么

上述解析了什么是对象，在JavaScript编程语言中，我们可以结合下面的例子理解。

例如：
```

var person = {//定义一个对象
name:"mm",
age:18,
job:"teacher",
}
person.job = "lawyer";//重设对象属性值
person.sex = "男";//增加对象属性
console.log(person.job);//lawyer 修改后的属性值
console.log(person.sex);//男 能访问到新增的属性
console.log(person)//输出整个对象

```



## 二、创建对象

### 1、构造函数

如果要创建多个person对象，是不是要写多遍？如果用上面的方法这样创建是的，那有什么办法避免写重复的代码？有的哦亲。JavaScript中有种叫做工厂模式的方法，就是大批量的生产对象。可是JavaScript又嫌弃说生产得到的对象不知道它的类型是什么。所以现在大家都是用构造函数模式，说是构造函数其实和普通的函数没啥区别，就是调用的时候需要“new”一下，不过它里面的方法和属性都指向这个构造函数自己，所以创建出来的对象其实就是这个方法的实例。保证了对象的类型。相当于是把一个对象封装进一个方法里面了。
书写：在构造函数中，因为借鉴其他OO的语言，所以函数名的第一个字母习惯大写，创建的属性对象都赋值给this对象，这里这个this指的是这个构造函数。
例如：

```
function newperson(name,age,sex){//工厂模式
var person = new Object;
person.name = name;
person.age = age;
person.sex = sex;
return person;
}
var person1 = newperson("luara",18,"女");//创建对象
var person2 = newperson("LL",25,"男");//创建对象
console.log(person1);//{name: "luara", age: 18, sex: "女"}

console.log("==================================");
function Clothes(color,price,address){//创建构造函数
this.color = color;
this.price = price;
this.address = address;
}
var clothes1 = new Clothes("red",250,"广东");//创建新的对象，把构造函数的作用域也就是this复制给新的对象，执行上面的函数体，返回一个新的函数。
console.log(clothes1);//Clothes {color: "red", price: 250, address: "广东"}
```



### 2、构造函数的存在问题

既然构造函数那么还用，那构造函数是不是完美的呢？当然不是完美的，而且存在的问题还不少。

**（1）**

首先来说一下定义在构造函数中的方法，因为每次新建一个对象，就”new”一个实例，实例对象可以用到构造函数中的方法没错，不过每次新建一个实例其实都创建了一个方法，因为只是那个方法名相同，函数是新建的，在批量创建实例的时候很废内存。

**（2）**

为了解决这个问题，我们可以把方法建在构造函数的外面，因为写在全局作用域中的方法中有个this指向函数的指针，方法之创建一次，实例可以执行任意次，并且确保了每个实例执行的都是同一个方法。可是，问题来了，外面的方法是构造函数的属性，并且只能被构造函数的实例调用，万一这个构造函数定义了很多这样的属性方法呢，都写在全局作用于中，除了构造函数的实例外，其他都不能调用，是不是不太科学了。

例如：
```
function Clothes(color,price,address){//创建构造函数
this.color = color;
this.price = price;
this.address = address;
this.saycolor = function(){//在构造函数内的函数方法
alert(this.color)
};
this.sayPrice = sayPrice;//函数方法写在构造函数外部
}
var clothes1 = new Clothes("red",250,"广东");//创建新的对象，把构造函数的作用域也就是this复制给新的对象，执行上面的函数体，返回一个新的函数。
var clothes2 = new Clothes("red",250,"广东");
console.log(clothes1);//Clothes {color: "red", price: 250, address: "广东"}

console.log(clothes1.saycolor == clothes2.saycolor);//false 不是用一个方法
function sayPrice(){//实例可以调用用一个方法，不过只能被实例调用
alert(this.price);
};
sayPrice()//undefined 这时候this指的是window
clothes1.sayPrice();//250 可以调用

```


### 3、解决问题

问题的解决办法就是要把属于对象的函数方法写在构造函数，在外面访问对象方法时候，领人反问到的是对象的同一个方法。我们在创建函数的时候都会有一个`prototype`原型属性，从字面上理解是新创建的对象实例的原来的原型对象。所以这个属性总是指向原型对象。有个`prototype`原型属性我们就可以把对象和方法都写在函数体里面封装起来了。不过创建的是一个空的构造函数，它的原型对象我们不知道名字，只能用`prototype`添加属性和方法。而新对象是构造函数的实例，所以也具有那些函数和方法。不过不设置的时候是不显示的。
怎么才能知道原型对象中有多少个属性和方法呢？我们可以运用`Object.keys( )`方法枚举，返回的是一个数组。


![](/assets/images/blog-images/JS/构造函数和对象.webp)

例如：
```
function Clothes(){//创建函数
};

//函数的原型对象属性；
Clothes.prototype.color = "red";
Clothes.prototype.price = 250;
Clothes.prototype.saycolor = function(){
alert(this.color);
};
var clothes1 = new Clothes();
clothes1.color = "blue";
console.log(clothes1);//blue 只有一个属性，因为创建的Clothes是空的函数，clothes1只是Clothes的一个实例，拥有Clothes的原型对象的方法。

//拥有全部原型对象的属性
var key = Object.keys(Clothes.prototype);//因为不知原型对象的名称是什么，所以用Object
console.log(key);//["color", "price", "saycolor"] 得到一个数组，元素是原型对象的属性

```


### 4、最简单的原型语法--constructor的运用

上面写法虽好，不过太多的重复了，我们可以把从复部分封装成一个对象，这个对象就是原型对象，不过封装成原型对象后constructor指针就会发生变化。不再指向构造函数了，而是指向原型对象（Object）。这样创建出来的实例不是构造函数的实例。这个不就简单了，在封装的原型独享中增加一个`constructor`属性指向构造函数不就得了。其实用什么名字作为原型对象的对象名都可以，用`Clothes.prototype`只是好标识，让人一看就明白是构造函数的原型对象。
重点是设置constructor属性。这个决定着这个对象是普通对象还是原型对象。
例如：
```
function Clothes(){//创建函数
};

Clothes.prototype = {//用Clothes.prototype字面量做原型对象名，目的是好表示，其实随意用一个也行
constructor : Clothes,//指向构造函数，成为原型对象，否则就是一个普通的对象
color:"red",
price:250,
saycolor:function(){
alert(this.color)
}
}
var clothes1 = new Clothes();
clothes1.color = "green";//Clothes {color: "green"}
console.log(clothes1)

```


### 5、构造函数和原型模式的结合

其实在实际使用过程中，上面的构造函数不可能是空的，可以在构造函数设置其他属性，然后在原型对象设置共享的对象和方法。为什么说共享，那是原型对象的特性，就是因为它有这个特性，所以才把方法放在原型属性里面，避免创建的对象实例用的不是同一个方法。我们在应用中，大多都是构造函数和原型模式相互结合，既简化了代码，又增强了性能。我们以后就这样用就对了。
例如：
```
function Clothes(address){//创建带参的构造函数
this.address = address;
};

Clothes.prototype = {//用Clothes.prototype字面量做原型对象名，目的是好表示，其实随意用一个也行
constructor : Clothes,//指向构造函数，成为原型对象，否则就是一个普通的对象
color:"red",
price:250,
saycolor:function(){
alert(this.color)
}
}

var clothes1 = new Clothes("深圳");//传入参数
clothes1.color = "green";//Clothes {color: "green"}
console.log(clothes1)

```



## 三、对象继承

进过上面解说的例子，相信你已经大概知道圆形对象是什么东西了，每创建一个函数，其实这个函数都是继承了原型对象的属性和方法的。再创建的实例，也会具有构造函数的属性和方法。只要使用到一个对象，都会具备他的属性和方法。
举个简单的例子：
```
function Man(name,age){
this.name = name;
this.age = age;
}
var man1 = new Man("小呵",15);
console.log(man1.name)//小呵 具备Man的属性和方法
```


这就是JavaScript中对象的创建和运用。在JavaScript中一切皆对象。掌握这个JavaScript特性才能玩转JavaScript。

推荐阅读：

[JavaScript-window对象常用属性和方法全集](https://muitlog.com/2019/11/27/javascript-window.html)



[ES6剪头函数及对象表达式](https://muitlog.com/2019/11/27/ES6%E5%89%AA%E5%A4%B4%E5%87%BD%E6%95%B0%E5%8F%8A%E5%AF%B9%E8%B1%A1%E8%A1%A8%E8%BE%BE%E5%BC%8F.html)


[vue中的增加删除修改接口请求数据操作](https://muitlog.com/2019/10/23/vue%E4%B8%AD%E7%9A%84%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E4%BF%AE%E6%94%B9%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C.html)