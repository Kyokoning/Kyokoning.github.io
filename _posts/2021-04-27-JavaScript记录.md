---
layout:     post
title:      "JavaScript记录"
subtitle:   ""
date:       2021-4-27 01:45:08
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - JavaScript
	- 前端
	- 学习存档
---

[TOC]

### 摘要

学习参考文献

[W3CSchool](https://www.w3cschool.cn/javascript/js-tutorial.html)

js：web编程语言

### 基础知识

#### 语法

HTML中，脚本必须位于\<script>和\</script>中间，脚本可以在\<body>和\<head>部分中。通常放在\<head>中，或者页面底部，这样就不会干扰页面的内容。

也可以把脚本保存在外部文件中，使用`<script src="scriptName.js"></script>`使用js文件。

老旧的实例会在\<script>标签中加入type="text/javascript"，现在不需要。因为js是所有浏览器和HTML5中的默认脚本语言。

字符串可以是单双引号的。

注释是`//`和`/**/`

大小写敏感

命名使用驼峰法

浏览器按照编写顺序依次执行每条语句

#### 输出

| 方法                                  | 简介                      | 例子                                                | 注释                                                         |
| ------------------------------------- | ------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| window.alert()                        | 弹出警告框                | `window.alert("你妈的");`                           |                                                              |
| document.getElementById(id).innerHTML | 使用innerHTML写入HTML元素 | `document.getElementById(id).innerHTML="修改段落";` | document.getElementById(id)来访问某个HTML元素，并使用innerHTML来获取或插入元素内容 |
| document.write()                      | 输出到HTML文档            | `document.write(Date());`                           | 向文档输出写内容。如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖。 |
| console.log()                         | 输出到控制台              | `console.log(c)`                                    | 在开发者模式（F12）中查看                                    |

#### 变量声明方法

```javascript
// 使用var定义变量，等号给变量赋值
var x, length;
x = "这是字符串捏";
length=6;

// 也可以这么写
var y = 7， z=8, job="nojob"; 

// 也可以跨行
var y = 7， 
z=8, 
job="nojob"; // 
```

#### 数据类型简介

JS是动态类型的，相同变量可以用作不同类型。

| 类型   | 用途                | 例子                                                         | 备注                                                         |
| ------ | ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 布尔值 |                     | `var x=true;`<br>`var y=false;`                              | 1. 其他对象使用`Boolean()`方法转换；<br>                     |
| string |                     |                                                              | 1. 使用`.length`属性访问长度<br>2. 其他对象使用`toString()`方法进行类型转换<br>3. 使用`eval()`方法可以计算string格式的表达式的值并返回数值 |
| number |                     |                                                              | 1. 正负无穷：`Infinity`/`Number.POSITIVE_INFINITY`和`-Infinity`/`Number.NEGATIVE_INFINITY`<br>2. `isNaN()`：如果某个变量可以转换为数值，返回`false`否则返回`true`<br>3. 其他对象使用`Number()`方法转换 |
| 数组   |                     | `var cars=new Array();`<br>`cars[0]="ss";`<br>`cars[1]="sa";`<br>或者<br>`var cars=["ss", "sa"];` |                                                              |
| 对象   | 一组数据∨功能的集合 | `var person={firstname:"John", lastname:"Doe", id:5566};`<br>对象属性的寻址方式：<br>`name=person.lastname;`<br>`name=person["lastname"];` |                                                              |
| null   | 清空变量            | `cars=null;`                                                 |                                                              |
#### 对象

在js中，对象是一种基本数据类型，可以看做是无序的数据集合，由若干个键值对构成。

```javascript
var o={
    name:'a'
}
```

key：所有的键名都是字符串，所以可以加或不加引号。如果是数字会自动转换成字符串。（如果键名不符合标识名条件，则必须加上引号）

##### 遍历对象的键值

```javascript
var o = {name:"a", age:"12"}
// 采用for...in方法
for (var i in o) {
    console.log(o[i])
}
// 查看所有键值，用Object.keys()方法：
var key = Object.keys(o)
```

##### 删除属性

```javascript
delete o.name
```

##### 检测属性是否存在与对象

```javascript
// 使用in关键字，自有属性和继承属性都被承认
name in o;
// hasOwnProperty()方法，只承认自有属性
o.hasOwnProperty("toString");
// !==undefined方法，自有和继承都被承认。这个方法在值为undefined的时候会出错
o.x!==undefined;
```

##### 序列化对象

即，将对象转换为字符串

```javascript
s = JSON.stringify(o); // s {"name":"a","age":12]}
p = JSON.parse(s) // s是o的深拷贝（即内容一样但是内存地址不同）
```

##### 构造函数

用于生成对象的函数。一个构造函数可以用于生成多个对象实例。

```javascript
function Car(color){
    this.color=color;
}
var c = new Car("red");
```





#### 函数

```javascript
// 方法1：
function functionname(a, b){
    执行代码
}

// 方法2：
var functionname = function(a, b) {执行代码};

// 方法3：匿名函数
(function() {执行代码}())

```

JS中函数的花括号是必须的：即使只有一个语句，也必须用花括号。

在函数内声明的变量是局部变量；函数外声明的是全局变量，网页上所有脚本和函数都可访问。全局变量会在页面关闭后被删除。

##### 函数形参默认值

```javascript
// 当用函数的时候传入的实参比函数声明时指定的形参个数要少，剩下的形参都将设置为undefined值。 为了保持好的适应性，一般应当给参数赋予一个合理的默认值。
function go(x, y){
    x = x || 1;
    y = y || 2;
}

// 
```

##### 可变长传入参数

```javascript
// 传入类数组对象
function go(x) {
    // 使用标识符arguments，它指向实参对象的引用，可通过数字下标访问参数值
    console.log(arguments[0]);
    console.log(arguments[1]);
    // arguments的length属性可以标识所包含元素的个数
    console.log(arguments.length);
}
go(1,2) // 传入参数的长度是可变的
```



#### 基础关键字

| 标识符       | 用途                                                         | 例子 | 备注 |
| ------------ | ------------------------------------------------------------ | ---- | ---- |
| break        | 跳出循环                                                     |      |      |
| try          | 实现错误处理，和catch一起使用                                |      |      |
| continue     | 跳过循环中的一个迭代。                                       |      |      |
| do ... while | 执行一个语句块，在条件语句为 true 时继续执行该语句块。       |      |      |
| for          | 在条件语句为 true 时，可以将代码块执行指定的次数。           |      |      |
| for ... in   | 用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。 |      |      |
| function     | 定义一个函数                                                 |      |      |
| if ... else  | 用于基于不同的条件来执行不同的动作。                         |      |      |
| return       | 退出函数                                                     |      |      |
| switch       | 用于基于不同的条件来执行不同的动作。                         |      |      |
| throw        | 抛出（生成）错误 。                                          |      |      |
| while        | 当条件语句为 true 时，执行语句块。                           |      |      |

