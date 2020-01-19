---
title: Java 中的package包作用域详解
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: java
key: 2019111901
---

## 一、package包

再之前的章节学习中，你也许会发现，当定义一个数组时Arrays时，会在编辑器上面自动的添加一行`import java.util.Arrays; `这个就是package包，说明这个数组类是`util.Arrays `包引入的。所以可以想到，在Java中，我们使用package来解决名字冲突的。一个类总是属于某个包，类名（比如Man）只是一个简写，真正的完整类名是`包名.类名`。
我们在定义class的时候，需要在第一行声明这个class属于哪个包。
添加了包名，你会发现项目目录的的包名也会跟着变。

例如：

```
package luo;

public class Main {
}
```

> 需要注意的是：包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。




## 二、包的作用域

同一个包的类，可以访问包作用域的字段和方法。即系不用`public、protected、private`修饰的字段和方法就是包作用域。

例如：

```
package luo;
public class Main {
    public static void main(String[] args) {
    Man m = new Man();
        m.hello(); // 可以调用，因为Main和Man在同一个包
    }
}

//如果是public class Man就不会被调用，因为不在包作用域
class Man {
// 包作用域:
    void hello() {
        System.out.println("Hello!");
    }
}
```


## 三、import

其实在引用其他类的时候，你也可以引用全名，不过很少人会这样做不，毕竟`报名+类名`写起来很复杂。所以一般人都会写简写，前提是用`import`引入。
在写import的时候，可以使用*，表示把这个包下面的所有class都导入进来。不过这样很难看出是哪个包的类了。

如果想导入一个类的全部静态方法和字段可以用`import static`。

例如：

```
// Person.javapackage ming;
// 导入完整类名:import mr.jun.Arrays;
public class Man{
    public void run() {
        Arrays arrays = new Arrays();
    }
}

```


## 四、编译包名和类

其实，Java编译器最终编译出的.class文件只使用完整类名。所以当编译器遇到一个class名称时，会去查找这个包下是否有这个类，`import`中是否包含这个类，`java.lang`中是否包含这个类。所以我们在命名类的时候尽量避免使用java中的同名类或者关键字。