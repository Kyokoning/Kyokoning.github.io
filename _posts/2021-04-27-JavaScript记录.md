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
| window.alert()                        | 弹出警告框                | `window.alert("你妈的");`                           | 类似的弹出警告窗方法还有`confirm()`和`prompt()`方法          |
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

可以使用`typeof`操作符来查看变量的数据类型

```javascript
typeof "John"                 // 返回 string
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number
typeof false                  // 返回 boolean
typeof [ 1,2,3,4]              // 返回 object
typeof {name: 'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (if myCar is not declared)
typeof null                   // 返回 object
```

这种方法无法查看Date属性或者Array属性，因为他们都返回object。

可以使用`constructor`属性返回js变量的构造函数，来查看对象是否为Date或者Array（构造函数包含字符串"Date"或者"Array"）：

```javascript
function isArray(myArray) {
    return myArray.constructor.toString().indexOf("Array") > -1;
}

function isDate(myDate) {
    return myDate.constructor.toString().indexOf("Date") > -1;
}
```

| 类型   | 用途                 | 例子                                                         | 备注                                                         |
| ------ | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 布尔值 |                      | `var x=true;`<br>`var y=false;`                              | 1. 其他对象使用`Boolean()`方法转换；<br>2. 可以用`Number()`方法将布尔值转换为数字 |
| string |                      | `var carname = "Volvo";`<br>`var carname = 'Volvo';//可以使用单引号或双引号`<br> | 1. 使用`.length`属性访问长度<br>2. 其他对象使用`String()`方法或者`toString()`方法进行类型转换：`String(123)`、`(123).toString()`<br>3. 使用`eval()`方法可以计算string格式的表达式的值并返回数值<br>4. `trim()`方法删除字符串两段的空白文字：`text.trim()`<br>5. `indexOf()`方法从字符串中寻找第一次出现指定值的索引，如果未找到则返回`-1`：`text.indexOf("Search")` |
| number |                      |                                                              | 1. 正负无穷：`Infinity`/`Number.POSITIVE_INFINITY`和`-Infinity`/`Number.NEGATIVE_INFINITY`<br>2. `isNaN()`：如果某个变量可以转换为数值，返回`false`否则返回`true`<br>3. 其他对象使用`Number()`方法转换 |
| 数组   |                      | `var cars=new Array();`<br>`cars[0]="ss";`<br>`cars[1]="sa";`<br>或者<br>`var cars=["ss", "sa"];` | 1. 增加数组                                                  |
| 对象   | 一组数据与功能的集合 | `var person={firstname:"John", lastname:"Doe", id:5566};`<br>对象属性的寻址方式：<br>`name=person.lastname;`<br>`name=person["lastname"];` |                                                              |
| null   | 清空变量             | `cars=null;`                                                 | 只有一个值的特殊类型                                         |
#### 对象

在js中，对象是一种基本数据类型，可以看做是无序的数据集合，由若干个键值对构成。

```javascript
var o={
    name:'a'
}
```

key：所有的键名都是字符串，所以可以加或不加引号。如果是数字会自动转换成字符串。（如果键名不符合标识名条件，则必须加上引号）

对象属性的寻址方式：两种，一种是`.`，另一种是`[]`

```javascript
name=person.lastname;
name=person["lastname"];
```

##### JSON

\* JSON（JavaScript Object Notation）的创建方式和创建对象的语法是一样的，实际上应该就是同一种东西吧。

将JSON的文本转换成JSON对象的方法：

```javascript
var text = '{ "employees" : [' +
'{ "firstName":"John" , "lastName":"Doe" },' +
'{ "firstName":"Anna" , "lastName":"Smith" },' +
'{ "firstName":"Peter" , "lastName":"Jones" } ]}';

var obj = JSON.parse(text);
```



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

##### 常见函数

| 名字                                              | 用途                                                         | 例子或备注                                                   |
| ------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| document.getElementById()                         | 根据id得到HTML对象。如果没有找到元素，则返回null<br>类似的还有`document.getElementsByTagName()`和`document.getElemntsByClassName()` | `ar x=document.getElementById("demo")`<br>`x.innerHTML="<a href='http://w3cschool.cn'>Visit w3cschool</a>";` |
| document.getElementById(*id*).*srcName=new value* | 可以改变HTML元素的属性                                       | `document.getElementById("image").src="landscape.jpg";`      |
| addEventListener()                                | 往HTML对象中加入事件监听                                     | `element.addEventListener("click", myFunction);`<br/>使用匿名函数来调用带参数函数：<br/>`elemnt.addEventListener("click", function(){myFunction(p1, p2);});` |
| Math.random()                                     | 随机生成[0,1)之间的浮点数                                    |                                                              |
| Date()                                            | 获得当前时间的Date对象                                       | Date对象的方法：`getDate()` `getDay()` `getHours()` `getMinutes()`等等 |
| void()                                            | 括号内的表达式会计算，但是不会返回值                         |                                                              |
| navigator.cookieEnabled                           | 查看Cookie是否可用                                           |                                                              |
| setInterval()<br>clearInterval()                  | setInterval()用于计时事件，间隔指定的毫秒数，不停地执行指定的代码<br>clearInterval()用于停止setInterval()方法执行的函数代码 | 每隔3s执行一次弹窗：<br>`var myVar=setInterval(function(){alert("Hello")},3000);`<br/>停止执行：<br>`clearInterval(myVar);` |
| setTimeout()<br>clearTimeout()                    | setTimeout()用于等待事件后执行代码<br>clearTimeout()用于取消该代码的执行 | 等待3s后执行：<br>`myVar=setTimeout(function(){alert("Hello")},3000);`<br>停止执行：<br>`clearTimeout(myVar);` |
| window.onload()                                   | 用于在网页加载完毕之后立即执行的操作。函数语法：<br>`window.onload = function() {Func1();Func2();Func3();...}` |                                                              |



#### 基础关键字

| 标识符       | 用途                                                         | 例子                                                         |
| ------------ | ----------------------------- | --------------------------------------------- |
| break        | 跳出循环。可以用于循环或者switch中。<br>也可以用标签和break、continue来精准地控制循环代码块。 |                                                              |
| continue     | 跳过循环中的一个迭代。只能用于循环。                         |                                                              |
| function     | 定义一个函数                                                 |                                                              |
| return       | 退出函数                                                     |                                                              |
| do ... while | 执行一个语句块，在条件语句为 true 时继续执行该语句块。       | ![image-20210509171641737](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171641737.png) |
| for          | 在条件语句为 true 时，可以将代码块执行指定的次数。           | ![image-20210509171605859](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171605859.png)<br>for的第一个语句用于初始化循环中所用变量，这是可选的，不用也可以。也可以初始化多个值。<br>`for (var i=0, len=cars.length;i<len;i++)`<br>`{document.write(cars[i]+"<br");}`<br>第三个语句用于增加初始变量的值，也是可选的。 |
| for ... in   | 用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。 | ![image-20210509171612333](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171612333.png)<br>`var person={fname:"John", lname:"Doe"}`<br>`for (x in person)`<br>`{txt = txt + person[x]}` |
| while        | 当条件语句为 true 时，执行语句块。                           | ![image-20210509171344688](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171344688.png) |
| if ... else  | 用于基于不同的条件来执行不同的动作。                         | ![image-20210509171158999](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171158999.png)<br>如果if语句只有一行代码，可以省略花括号：<br>`if(i==3) break;`<br>记得一定要加条件表达式的括号！！！！不加括号无法识别的。 |
| switch       | 用于基于不同的条件来执行不同的动作。                         | ![image-20210509171221555](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509171221555.png) |
| try          | 实现错误处理，和catch一起使用                                | ![image-20210509225819067](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509225819067.png) |
| throw        | 抛出（生成）错误 。                                          | ![image-20210509225941432](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509225941432.png)<br>![image-20210509230003904](https://raw.githubusercontent.com/Kyokoning/image-bed/dev/img/blog-img/image-20210509230003904.png) |

#### 运算符

| 运算符          | 描述       |
| --------------- | ---------- |
| &&              | and        |
| \|\|            | or         |
| !               | not        |
| (condition)?a:b | 条件运算符 |

#### HTML事件

| 事件          | 描述                                         |
| ------------- | -------------------------------------------- |
| onclick       | 用户点击该HTML元素                           |
| onchange      | HTML元素改变（比如填表单之后鼠标离开表单？） |
| （onmouseover | 用户在HTML元素上移动鼠标                     |
| onmouseout    | 用户从HTML元素上移开鼠标                     |
| onkeydown     | 用户按下键盘按键                             |
| onload        | 浏览器已完成页面的加载                       |

例子：

```HTML
<button onclick="this.innerHTML=Date()">现在的时间是?</button>
<!--其中，this指向HTML元素自身，onclick的时候会改变该按钮的显示文字-->
```

#### DOM

文档对象模型（Document Objsct Model）。

#### Cookie

一个Cookie的设定和读取例子：

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>W3Cschool教程(w3cschool.cn)</title>
</head>
<head>
<script>

// 根据传入的用户名值cname和cookie存续日期长度exdays设定cookie
function setCookie(cname,cvalue,exdays){
    var d = new Date();
    d.setTime(d.getTime()+(exdays*24*60*60*1000));
    var expires = "expires="+d.toGMTString()+";";
    window.alert(cname+"="+cvalue+"; "+expires)
    document.cookie = cname+"="+cvalue+"; "+expires;
}

// 从一堆cookie中找到cname对应的值，即填入的用户名。
function getCookie(cname){
    var name = cname + "=";
    var ca = document.cookie.split(';');
    for(var i=0; i<ca.length; i++) {
        var c = ca[i].trim();
        if (c.indexOf(name)==0) return c.substring(name.length,c.length);
    }
    return "";
}
// 查看cookie，如果有username对应的内容，则显示弹窗，否则要求用户填入名字，更新cookie。
function checkCookie(){
    var user=getCookie("username");
    if (user!=""){
        alert("Welcome again " + user);
    }
    else {
        user = prompt("Please enter your name:","");
        if (user!="" && user!=null){
            setCookie("username",user,30);
        }
    }
    displayCookie()
}
// 调试用，查看当前的cookie
function displayCookie() {
    var x = document.getElementById("test");
    x.innerHTML=document.cookie;
}
// 删除cookie，原生js实际上没法直接使用时间expires删除cookie，因此直接将username置空。
function deleteCookie() {
    document.cookie = "username=; expires=Thu, 18 Dec 2013 12:00:00 GMT;";
    displayCookie()
}
</script>
</head>
    
<body onload="checkCookie()">
    <button type="button" onclick="deleteCookie()">
点我删除cookie</button>
    <p id="test">test</p>
</body>
    
</html>
```

