

# 1、什么是JavaScript

## 1.1、概述

JavaScript是一门世界上最流行的脚本语言

Java,JavaScript没有关系

一个合格的后端人员，必须精通JavaScript

## 1.2、历史

ECMAScript它可以理解为JavaScript的一个标准

最新版本已经到ES6版本~

但是大部分浏览器还只停留在支持ES5代码上

开发环境--线上环境，版本不一致

# 2、快速入门

## 2.1、引入JavaScript

1、内部标签

```html
<script>
    alert("hello,world");
</script>
```

2、外部引入

例如有一个script.js

``` javascript
//.....
```

在另一个html中

```html
<script src="JavaScript.js"></script>
```



测试代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    <script>-->
<!--        alert("hello,world");-->
<!--    </script>-->

<!--    外部引入-->
<!--    注意：script标签必须成对出现-->
    <script src="JavaScript.js"></script>
<!--    不用显示定义type.也默认就是JavaScript-->
    <script type="text/javascript"></script>

</head>
<body>

</body>
</html>
```

## 2.2、基本语法入门

```html
<script>
    //1.定义变量 变量类型 变量名=变量值
    var num=61;
    // alert(num);
    //2.条件控制
    if (num>60&&num<70){
        alert("60-70");
    }else if (num>70&&num<80){
        alert("70-80")
    }else {
        alert("other")
    }
    // console.log(num) 在浏览器的控制台打印变量！sout();

</script>
```

浏览器必备调试须知：

![image-20210330231813585](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210330231813585.png)

## 2.3、数据类型

数值，文本，图形，音频，视频.........



变量

var 王者荣耀=‘倔强青铜'

number

js不区分小数和整数，**number**

``` javascript
123//整数123
123.1//浮点数123.1
1.233e3//科学计数法
-99//负数
NaN//not a number
Infinity//表示无限大
```

**字符串**

"abc" ‘abc’

‘\n’

**布尔值**

true，false

**逻辑运算**

``` javascript
&& 	两个都为真，结果为真
||	一个为真，结果为真
!	相反
```

比较运算符！！！重要！

``` 
=
==		等于(类型不一样，值一样，也会判断为true)
===		绝对等于(类型一样，值一样，结果为true)
```

这是一个js的缺陷，坚持不要使用==比较

须知：

- NaN===NaN ，这个与所有的数值都不相等，包括自己
- 只能通过isNaN(NaN)来判断这个数是否是NaN

浮点数问题

```javascript
console.log((1 / 3) === 1 - (2 / 3));
```

尽量避免使用浮点数进行运算，存在精度问题！

``` html
console.log(Math.abs(1 / 3 - (1 - (2 / 3))) < 0.0000000001);
```



**null和undefined**

- null空

- undefined未定义



数组

Java的数组必须是一系列相同类型的对象，但是JS中不需要这样

```js
// 保证代码的可读性，尽量使用[]
var arr=[1,2,3,4,5,"hello",null,true]
new Array(1,2,3,4,5,"hello",null,true);
```

取数组下标：如果越界了，就会

``` html
undefine 
```

对象

对象是大括号，数组是中括号。

每个属性之间使用逗号隔开，最后一个不需要

```javascript
var person={
    name:"czl",
    age:20,
    target:['a','b','c']
}
```

取对象的值

``` html
person.target
> ["a", "b", "c"]
```

## 2.4、严格检查格式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
            前提：IDEA需要设置支持ES6语法
            'use strict';严格检查模式，预防JavaScript的随意性导致产生的一些问题
            必须写在JavaScript的第一行!
            局部变量件一都是用let去定义~
    -->
    <script>
        'use strict';
        // 全局变量
        // i=1;
        j=1;
        // ES6 中let
    </script>
</head>
<body>

</body>
</html>
```

# 3、数据类型

## 3.1、字符串

**1、正常字符串我们使用单引号，或者双引号包裹**

**2、注意转义字符**

``` 
\'		转义
\n		换行
\t		tab
\u4e2d	\u#### Unicode字符
\x41	Asc11字符
```

**3、多行字符串编写**

```
// tab键上面的反引号可以写多行
var msg=`
dsjakdkhjsahkdjlsa
dsahjkdjkshadhsjkslakd
dshjkajdhsakjdsa
`
console.log(msg);
```

**4、模板字符串**

```
// tab键上面的反引号可以写多行
let name='czl';
let age=3;
let msg=`你好啊,${name}`
console.log(msg);
```

**5、字符串长度**

``` 
str.length
```

**6、字符串的可变性，不可变**

string是不可变的

stringbuffer和stringbuilder

**7、大小写转换**

``` 
//注意，这里是方法，不是属性了
console.log(some.toUpperCase())
console.log(some.toLowerCase())
```

**8、console.log(some.indexOf('c'))**

**9、console.log(some.substring(0,2))**

``` 
[)
some.substring(0,2)//从第0个到第1个
some.substring(0)//从第0个到最后一个
```

## 3.2、数组

Array可以包含任意的数据类型

``` 
var arr=[1,2,3,4,5,6]//通过下标取值和赋值
arr[0]
arr[0]=1
```

1、长度

``` 
arr.length
```

注意：假如给arr.length赋值，数组大小就会发生变化~，如果赋值过小，元素就会丢失

2、indexof

``` 
arr.indexOf(2)
1
```

字符串的”1“和数字1是不同的

**3、slice()**截取Array的一部分，返回一个新数组，类似于String中的substring

4、push() 和 pop() 

``` 
push压入到尾部
pop弹出尾部的一个元素
```

5、unshift() ,shift()头部

``` 
unshift压入到头部
shift弹出头部的一个元素
```

6、排序sort()

``` javascript
(10) [1, 2, 3, 4, 5, 6, "a", "b", "c", "a"]
arr.sort()
(10) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c"]
```

7、元素反转

``` javascript
(10) [1, 2, 3, 4, 5, 6, "a", "b", "c", "a"]
arr.reverse()
(10) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c"]
```

8、concat()

``` javascript
arr
(10) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c"]
arr.concat([1,1,1])
(13) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c", 1, 1, 1]
arr
(10) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c"]
```

注意：concat（）并没有修改数组，只是会返回一个新的数组

9、连接符join

打印拼接数组，使用特定的字符串连接

``` javascript
arr
(10) [1, 2, 3, 4, 5, 6, "a", "a", "b", "c"]
arr.join('-')
"1-2-3-4-5-6-a-a-b-c"
```

10、多维数组

``` javascript
num=[[0,1],[2,3]]
num[0][1]
1
```

数组：存储数据（如何存，如何取，方法都可以自己实现！）

## 3.3、对象

若干个键值对

```javascript
var 对象名={
	属性名：属性值，
	属性名：属性值，
	属性名：属性值
}
//定义了一个person对象，它有四个属性！
var person={
    name:"czl",
    age:3,
    email:"793570029.com",
    score:0
}
```

js中的对象，{.....}表示一个对象，键值对描述属性XXXX:XXXX,多个属性之间使用逗号隔开，最后一个属性不加逗号！

JavaScript中的所有的键都是字符串，值是任意对象！

1、对象赋值

``` js
person.age
3
person.name
"czl"
```

2、使用一个不存在的对象属性，不会报错！undefined

``` 
person.sss
undefined
```

3、动态的删减属性,通过delete删除对象的属性

``` javascript
person
{name: "czl", age: 3, email: "793570029.com", score: 0}
delete person.name
true
person
{age: 3, email: "793570029.com", score: 0}
```

4、动态的添加,直接给新的属性添加值即可

``` javascript
person.haha="haha"
"haha"
person
{age: 3, email: "793570029.com", score: 0, haha: "haha"}
```

5、判断属性值是否在这个对象中！xxx in xxx!

``` javascript
"age"in person
true
//继承
"toString" in person
true
```

6、判断一个属性是否是这个对象自身拥有的

``` javascript
person.hasOwnProperty('age')
true
person.hasOwnProperty('toString')
false
```

## 3.4、流程控制

if 判断

``` javascript
var age=3;
if (age>3){//第一个判断
    alert("haha");
}else if (age<5){//第二个判断
    alert("kuwa~");
} else {//否则，
    alert("kuwa~");
}
```

while循环，避免程序死循环

```javascript
while (age<100){
    age++;
    console.log(age);
}

```

for循环

```javascript
for (let i = 0; i < 100; i++) {
    console.log(i);
}
```

**forEach数组循环**

ES 5.1 引入的

``` javascript
var age=[1,1,2,2,3,3,12,321,4,2,44];
age.forEach(function (value) {
 console.log(value);
})
```

for in

```javascript
//for(var index in object){}
for (let num in age){
    if (age.hasOwnProperty(num)){
        console.log("存在");
        console.log(age[num]);
    }
}
```

## 3.5、Map和Set

ES6的新特性~

Map：

```javascript
// ES6,Map
// 学生的成绩，学生的名字
// var names=["tom","jack","thx"];
// var scores=[100,99,98];
var map=new Map([['tom',100],['jack',90],['czl',60]]);
var name=map.get('tom');//通过key获得value
map.set('admin',123)
console.log(name);
```

Set：无序不重复的集合

```javascript
var set=new Set([2,3,3,3,3,3,3,3,3]);//set可以去重
set.add(1);//添加
set.delete(2);//删除
console.log(set.has(3))//是否包含某个元素
```

## 3.6、iterator

ES6新特性

遍历数组

```javascript
var arr=[3,4,5]
//下标
for (let arrKey in arr) {
    console.log(arrKey);
}
//具体的值
for (let arrKey of arr) {
    console.log(arrKey);
}
```

遍历map

```javascript
var map=new Map([['tom',100],['jack',90],['czl',60]]);
for (let mapElement of map) {
    console.log(mapElement);
}
```

遍历Set

```javascript
var set=new Set([5,6,7]);
for (let number of set) {
    console.log(number);
}
```

# 4、函数及面向对象

方法：对象（属性，方法）

函数：

## 4.1、函数定义及变量作用域

**定义方式一**

绝对值函数

```javascript
function abs(x){
    if (x>0){
        return x;
    }else return -x;
}
```

一旦执行到return代表函数结束，返回结果。

如果没有执行return，函数执行完也会返回结果，结果就是undefined

**定义方式二**

``` javascript
var abs=function(x){
    if (x>0){
        return x;
    }else return -x;
}
```

function(x){...}这是一个匿名函数类。但是可以把结果赋值给abs，通过abs就可以调用函数！

方式一和方式二等价！

> ​	调用函数

``` js
abs(10)//10
abs(-10)//10
```

参数问题：JavaScript可以传任意个参数，也可以不传递参数~

参数进来是否存在的问题？

假设不存在参数，怎么规避？

 ``` javascript
var abs=function(x){
    //手动抛出异常来判断
    if (typeof x!=='number'){
        throw 'not a number';
    }
    if (x>0){
        return x;
    }else return -x;
}
 ```

> arguments

arguments是一个js免费赠送的关键字

代表，传递进来的所有的参数，是一个数组

```javascript
var abs=function(x){
    console.log("x=>" + x);
    for (var i=0;i<arguments.length;i++){
        console.log(arguments[i]);;
    }
    //手动抛出异常来判断
    if (typeof x!=='number'){
        throw 'not a number';
    }
    if (x>0){
        return x;
    }else return -x;
}
```

问题：arguments包含所有的参数，我们有时候想使用多余的参数来进行附加操作。需要排除已有参数~

> rest

以前：

```js
if (arguments.length>2){
    for (var i=2;i<arguments.length;i++){
        //....
    }
}
```

ES6引入的新特性，获取除了已经定义的参数之外的所有参数~......

```javascript
function aaa(a,b,...rest){
    console.log("a=>" + a);
    console.log("b=>" + b);
    console.log(rest);
    }
```

rest参数只能写在最后面，必须用...标识

## 4.2、变量的作用域

在JavaScript中，var定义的变量实际是有作用域的。

假设在函数体中声明，则在函数体外不可以使用~（非要想实现的话，后面可以研究一下闭包）

``` javascript
function czl(){
    var x=1;
    x=x+1;
}
x=x+1;//Uncaught ReferenceError: x is not defined
```

如果两个函数使用了相同的变量名，只要在函数内部，就不冲突。

```js
function czl1(){
    var x=1;
    x=x+1;
}
function czl2(){
    var x='a';
    x=x+1;
}
```

> 内部函数可以访问外部函数的成员,反之则不行

```js
function czl(){
    var x=1;
    //内部函数可以访问外部函数的成员,反之则不行
    function czl1(){
        var y=x+1;//2
    }
    var z=y+1;//Uncaught ReferenceError: y is not defined
}
```

假设，内部函数变量喝外部函数的变量，重名！

```js
function czl(){
    var x=1;
    function czl1(){
        var x ="A";
        console.log('inner'+x);
    }
    console.log('outer' + x);
    czl1();
}
czl();
```

假设在JavaScript中函数查找变量从自身函数开始~，由“内”向"外"查找.假设外部存在这个同名的函数变量，则内部函数会屏蔽外部函数的变量。

> 提升变量的作用域

```js
function czl(){
    var x="x"+y;
    console.log(x);
    var y="y";
}
```

结果：xundefined

说明：js执行引擎，自动提升了y的声明

```js
function czl(){
    var y;
    var x="x"+y;
    console.log(x);
    y = "y";
}
```

这个是在JavaScript建立之初就存在的特性。养成规范：所有的变量定义都放在函数的头部，不要乱放，便于代码维护；

```js
function czl(){
    var x=1,
        y=x+1,
        z,i,a;//undefined
    //之后随意用
}
```

> 全局函数

```js
// 全局变量
x=1;
function f(){
    console.log(x);
}
f();
console.log(x);
```

全局变量windows

```js
var x="xxx";
alert(x);
alert(window.x);//默认所有的全局变量，都会自动绑定在window对象下
```

alert（）这个函数本身也是一个window变量；

```js
var x="xxx";

alert(x);

var old_alert =window.alert;//默认所有的全局变量，都会自动绑定在window对象下
// old_alert(x);
window.alert=function (){};

//发现alert失效了
alert(x);

// 恢复
window.alert=old_alert;
window.alert(x);
```

JavaScript实际上只有一个全局作用域，任何变量（函数也可以视为变量），假设没有在函数作用范围内找到，就会向外查找，如果在全局作用域都没有找到，报错ReferenceError

> 规范

由于我们所有的全局变量都会绑定到我们的Windows上，如果不同的js文件，使用了相同的全局变量，冲突~

如何能够减少冲突？

```js
// 唯一全局变量
var czl={};
// 定义全局变量
czl.name='czl';
czl.add=function (a,b){
    return a+b;
}
```

把自己的代码全部放入自己定义的唯一空间名字中，降低全局命名冲突的问题。

jQuery

> 局部作用域

```js
function aaa(){
    for (var i = 0; i < 100; i++) {
        console.log(i);
    }
    console.log(i);//i出了这个作用域还可以用
}
```

ES6 let关键字，解决局部作用域冲突问题！

```js
function aaa(){
    for (let i = 0; i < 100; i++) {
        console.log(i);
    }
    console.log(i);//Uncaught ReferenceError: i is not defined
}
```

建议大家都是使用let去定义局部作用域的变量；

> const

在ES6之前，怎么定义常量：只要用全部大写字母命名的变量就是常量；建议不要修改这样的值

```js
var PI='3.14';
console.log(PI);
PI='223';//可以改变这个值
console.log(PI);
```

在ES6引入了常量关键字

```js
const PI='3.14';//只读变量
console.log(PI);
PI='223';
```

## 4.3、方法

> 定义方法

方法就是把函数放在对象的里面，对象只有两个东西：属性和方法

```js
var czl={
    name:"czl",
    birth:2000,
    // 方法
    age:function (){
        // 今年-出生的年
        var now=new Date().getFullYear();
        return now-this.birth;
    }
}
czl.age//属性
ƒ (){
            // 今年-出生的年
            var now=new Date().getFullYear();
            return now-this.birth;
        }
czl.age()//方法一定要带（）
21
```

this代表什么？

```js
function getAge(){
    // 今年-出生的年
    var now=new Date().getFullYear();
    return now-this.birth;
}

var czl={
    name:"czl",
    birth:2000,
    // 方法
    age:getAge
}
//czl.age()成功
//getAge()失败
```

this是无法指向的，是默认指向调用它的那个对象；

> apply

在js中可以控制this指向！

```js
function getAge(){
    // 今年-出生的年
    var now=new Date().getFullYear();
    return now-this.birth;
}

var czl={
    name:"czl",
    birth:2000,
    // 方法
    age:getAge
}
//czl.age()成功
//getAge()失败
getAge.apply(czl,[])//this，指向了czl，参数为空
```











## 4.3、闭包（难点）

## 4.4、箭头函数（新特性）

## 4.5、创建对象

## 4.6、class继承（新特性）

## 4.7、原型链继承（难）

# 5、内部对象

> 标准对象

``` js
typeof 1
"number"
typeof "1"
"string"
typeof NaN
"number"
typeof true
"boolean"
typeof []
"object"
typeof {}
"object"
typeof Math.abs
"function"
typeof undefined
"undefined"
```

## 5.1、data

> **基本使用**

```js
var now=new Date();
now.getFullYear();//年
now.getMonth();//月
now.getDate();//日
now.getDay();//星期几
now.getHours();//时
now.getMinutes();//分
now.getSeconds();//秒
now.getTime();//时间戳 全世界统一
console.log(new Date(1617342504489));
console.log(now);
```

转换

``` js
console.log(new Date(1617342504489));;
VM34:1 Fri Apr 02 2021 13:48:24 GMT+0800 (中国标准时间)
undefined
now.toLocaleString
ƒ toLocaleString() { [native code] }
now.toLocaleString()
"2021/4/2下午1:48:24"
now.toGMTString
ƒ toUTCString() { [native code] }
now.toGMTString()
"Fri, 02 Apr 2021 05:48:24 GMT"
```

## 5.2、JSON

> json是什么

早期，所有数据传输习惯使用XML文件

- [JSON](https://baike.baidu.com/item/JSON)([JavaScript](https://baike.baidu.com/item/JavaScript) Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式
- 简洁和清晰的**层次结构**使得 JSON 成为理想的数据交换语言。 
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在JavaScript一切皆为对象，任何js支持的类型都可以使用json来表示；

格式：

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用key：value

JSON字符串和JS对象的转化

```js
var user={
    name:'czl',
    age:3,
    sex:"男"
}
// 对象转化json字符串{"name":"czl","age":3,"sex":"男"}
var jsonUser=JSON.stringify(user)
// json字符串转化为对象 里面单，外面双，里面双，外面单。
var obj=JSON.parse('{"name":"czl","age":3,"sex":"男"}');
```

很多人搞不清楚，JSON和JS对象的区别

``` js
var obj={a:'hello',b:'hellob'};
var json='{"a":"hello","b":"hellob"}'
```

## 5.3、Ajax

- 原生的js写法 xhr异步请求
- jQuey封装好的方法$("#name").ajax("")
- axios请求

# 6、面向对象编程

## 6.1、什么是面向对象

JavaScript，Java，c#....面向对象；JavaScript有些区别！

- 类：模板 原型对象
- 对象：具体的实例

在JavaScript这个需要大家换一个思维方式！

原型：

```js
var user={
    name:'czl',
    age:3,
    sex:"男",
    run:function (){
        console.log(this.name + "run...");
    }
};

var xiaoming={
    name:"xiaoming"
};

//小明的原型是student
xiaoming.__proto__=user;

var Bird={
    fly:function (){
        console.log(this.name + "fly...");
    }
};
//原型更改为鸟
xiaoming.__proto__=Bird;
```

> class继承
>

class关键字，是在ES6中引入的

1、定义一个类，属性，方法

```js
// 定义一个学生的类
class student{
    constructor(name) {
        this.name=name;
    }
    hello(){
        alert("hello");
    }
}
var xiaoming=new student("xiaoming");
var xiaohong=new student("xiaohong");
xiaoming.hello
```

2、继承

```js
<script>
    // function student(name){
    //     this.name=name;
    // }
    // //给student新增一个办法
    // student.prototype.hello=function (){
    //     alert("hello")
    // };

    // ES6 之后======================================
    // 定义一个学生的类
    class student{
        constructor(name) {
            this.name=name;
        }
        hello(){
            alert("hello");
        }
    }
    class xiaostudent extends student{
        constructor(name,grade) {
            super(name);
            this.grade=grade;
        }
        mygrade(){
            alert("我是一名小学生")
        }
    }
    var xiaoming=new student("xiaoming");
    var xiaohong=new xiaostudent("xiaohong",1);
</script>
```

本质：查看对象原型

![image-20210402162536115](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210402162536115.png)

> 原型链

_ proto _

![image-20210402163114123](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210402163114123.png)

# 7、操作Bom对象（重点）

> 浏览器介绍

BOM：浏览器对象模型

JavaScript和浏览器关系？

JavaScript诞生就是为了能够让他在浏览器中运行！

BOM：浏览器对象模型

- IE 6~11
- Chrome
- Safari
- FireFox
- Opera



三方

- QQ浏览器
- 360浏览器

## window（重要）

window代表 浏览器窗口

``` javascript
window.alert("11")
undefined
window.innerHeight
420
window.outerHeight
1089
window.innerHeight
473
window.innerWidth
1773
window.outerWidth
1612
//大家可以调整浏览器窗口试试...
```



## Navigator

Navigator，封装了浏览器的信息

``` js
navigator.appCodeName
"Mozilla"
navigator.product
"Gecko"
navigator.appVersion
"5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36"
navigator.userAgent
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36"
navigator.platform
"Win32"
```

大多数时候，我们不会使用navigator对象，因为会被人为修改！

不建议使用这些属性来判断和编写代码。

## screen

代表屏幕尺寸

``` js
screen.width
2560
screen.height
1440
```

## location（重要）

location代表当前页面的URL信息

```js
location代表当前页面的URL信息
host: "www.baidu.com"
href: "https://www.baidu.com/?tn=02003390_2_hao_pg"
protocol: "https:"
location.reload()//刷新网页
//设置新的地址
location.assign('https://ai.taobao.com/?pid=mm_130402922_1111150093_109790500145&union_lens=lensId%3APUB%401585398442%400b0b0e45_0e0f_171211c6ac6_04ba%4001')
```

## document

document代表当前的页面，HTML DOM文档树

``` js
document.title
"百度一下，你就知道"
document.title='文档'
"文档"
```

获取具体的文档树节点

```js
<body>
<dl id="app">
    <dt>Java</dt>
    <dd>JavaSE</dd>
    <dd>JavaEE</dd>
</dl>
<script>
    var dl=document.getElementById("app");
</script>
```

## cookie

获得cookie

``` 
document.cookie
""
```

劫持cookie原理

www.taobao.com

```js
<script src="aa.js"></script>
<!--恶意人员获取你的cookie上传到他的服务器-->
```

服务器端可以设置cookie：httpOnly

## history

history代表浏览器的历史记录

``` 
history.back()//后退
history.forward()//前进
```

# 8、操作Dom对象（重点

DOM：文档对象模型

> 核心
>

浏览器网页就是一个Dom树形结构！

- 更新：更新Dom节点
- 遍历dom节点：得到dom节点
- 删除：删除一个Dom节点
- 添加：添加一个新的节点

要操作一个Dom节点，就必须要先获得这个Dom节点

> 获得Dom节点

```js
//对应CSS选择器
var h1=document.getElementsByTagName('h1');
var p1=document.getElementById('p1');
var p2=document.getElementsByClassName('p2');
var father=document.getElementById('father')

var childrens=father.children;//获取父节点下的所有子节点
//father.firstChild
//father.lastChild
```

这是原生代码，之后我们尽量都是用jQuery();

> 更新节点

操作文本

- id1.innerText="sssssss"修改文本的值
- ![image-20210402174354318](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210402174354318.png)

操作CSS

``` js
id1.style.color='yellow'//属性使用 字符串 包裹
id1.style.fontSize='20px'//-转 驼峰命名问题
id1.style.padding='2em'
```

> 删除节点

删除节点的步骤：先获取父节点，在通过父节点删除自己

``` html
<div id="father">
    <h1>标题一</h1>
    <p id="p1">p1</p>
    <p class="p2">p2</p>
</div>
<script>
    var self=document.getElementById('p1');
    var father=p1.parentElement;
    father.removeChild(p1);
</script>
```

注意：删除多个节点的时候，children是在时刻变化的，删除节点的时候一定要注意！



> 插入节点

我们获得了某个Dom节点，假设这个Dom节点是空的，我们通过innerHTML就可以增加一个元素了，但是这个Dom节点已经存在元素了，我们就不能这样干了！会产生覆盖。



追加

```html
<p id="js">javascript</p>
<div id="list">
    <p id="se">javase</p>
    <p id="ee">javaee</p>
    <p id="me">javame</p>
</div>
<script>
    var js = document.getElementById('js');
    var list=document.getElementById('list');
    list.append(js)//追加到后面
</script>
```

效果：

![image-20210405124907455](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210405124907455.png)

> 创建一个新的标签，实现插入

```html
<script>
    var js = document.getElementById('js');//已经存在的节点
    var list=document.getElementById('list');
    //通过js 创建一个新的节点
    var element = document.createElement('p');//创建一个p标签
    element.id='czl';
    element.innerText='hello,czl';
    list.appendChild(element);
</script>
```

```html
<script>
    var js = document.getElementById('js');//已经存在的节点
    var list=document.getElementById('list');
    //通过js 创建一个新的节点
    var element = document.createElement('p');//创建一个p标签
    element.id='czl';
    element.innerText='hello,czl';
    //创建一个标签节点 (通过这个属性，可以设置任意的值）
    var script = document.createElement('script');
    script.setAttribute('type','text/javascript')
    //可以创建一个style标签
    var mystyle=document.createElement('style');//创建一个空style标签
    mystyle.setAttribute('type','text/css');
    mystyle.innerHTML='body{background-color:chartreuse;}';//设置标签内容
    document.getElementsByTagName('body')[0].appendChild(mystyle)
</script>
```

> insert

```js
var ee=document.getElementById('ee');
var js=document.getElementById('js');
var list=document.getElementById('list');
//要包含的节点.list.insertBefore(newNode,targetNode);
list.insertBefore(js,ee);
```

# 9、操作表单（验证）

> 表单是什么 form DOM树

- 文本框 	text
- 下拉框    <select>
- 单选框    radio
- 多选框    checkbox
- 隐藏域    hidden
- 密码框    password
- ....

表单的目的：提交信息



> 获得要提交的信息

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<form action="post">
    <p>
        <span>用户名：</span><input type="text" id="username">
    </p>
<!--    多选框的值，就是定义好的value-->
    <p>
        <span>性别：</span>
        <input type="radio" name="sex" value="man" id="boy">男
        <input type="radio" name="sex" value="woman" id="girl">女
    </p>
</form>

<script>

    var input_text = document.getElementById('username');
    var boy_radio = document.getElementById('boy');
    var girl_radio = document.getElementById('girl');

    //得到输入框的值
    input_text.value;
    //修改输入框的值
    input_text.value='111';
    //对于单选框，多选框等等固定的值，boy_radio.value只能去到当前的值
    boy_radio.checked;//查看返回的结果，是否为true，如果为true，则被选中~
    boy_radio.checked=true;//赋值
</script>

</body>
</html>
```

> 提交表单。md5加密密码，表单优化

```html
<body>
<!--
表单绑定提交事件
onsubmit=绑定一个提交检测的函数，true false
将这个结果返回给表单，使用onsubmit接收
-->
<form action="https://www.baidu.com/" method="post" onsubmit="return aaa()">
    <p>
        <span>用户名：</span><input type="text" id="username" name="username">
    </p>
    <p>
        <span>密码：</span><input type="password" id="input-password">
    </p>
    <input type="hidden" id="md5-password" name="password">
<!--    绑定事件 onclick被点击-->
    <button type="submit" onclick="aaa()">提交</button>
</form>
<script>
    function aaa(){
        let username = document.getElementById('username');
        let password = document.getElementById('input-password');
        let md5password = document.getElementById('md5-password');
        md5password.value=md5(password.value);
        //可以校验判断表单内筒，true就是通过提交，false阻止提交。
        return true;
    }
</script>
</body>
```

# 10、jQuery

JavaScript

jQuery库，里面存在大量的JavaScript函数

> 获取jQuery

封装

公式：$(选择器).事件(事件函数)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    CDN引入-->
    <script crossorigin="anonymous" integrity="sha512-n/4gHW3atM3QqRcbCn6ewmpxcLAHGaDjpEBu4xZd47N0W2oQ+6q7oc3PXstrJYXcbNU1OHdQ1T7pAP+gi5Yu8g==" src="https://lib.baomitu.com/jquery/3.6.0/jquery.js"></script>
</head>
<body>

</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    CDN引入-->
<!--    <script crossorigin="anonymous" integrity="sha512-n/4gHW3atM3QqRcbCn6ewmpxcLAHGaDjpEBu4xZd47N0W2oQ+6q7oc3PXstrJYXcbNU1OHdQ1T7pAP+gi5Yu8g==" src="https://lib.baomitu.com/jquery/3.6.0/jquery.js"></script>-->
    <script src="../lib/jquery-3.6.0.js"></script>
</head>
<body>

<!--
公式：$(selector).action()
-->
<a href="" id="test-jquery">点我</a>

<script>
    //选择器就是CSS选择器
    $('#test-jquery').click(function (){
        alert('hello,jquery')
    })
</script>
</body>
</html>
```

> 选择器

```js
// 原生的js，选择器少，麻烦不好记
// 标签
document.getElementsByTagName();
// id
document.getElementById();
// 类
document.getElementsByClassName();

// jQuery css中的选择器它全部都能用
$('p').click()//标签选择器
$('#id1').click()//id选择器
$('.class1').click()//class选择器
```

文档工具站：https://jquery.cuishifeng.cn/



> 事件

鼠标事件，键盘事件，其他事件。

![image-20210407001407963](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210407001407963.png)



> 事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="../lib/jquery-3.6.0.js"></script>
    <style>
        #divMove{
            width: 500px;
            height: 500px;
            border: 1px solid red;
        }
    </style>
</head>
<body>

<!--    要求：获取鼠标当前的一个坐标-->
mouse:<span id="mouseMove"></span>
<div id="divMove">
    在这里移动鼠标试试
</div>

<script>
    // 当网页元素加载完毕之后，响应事件
    $(function () {
        $('divMove').mousemove(function (e) {
            $('#mouseMove').text('x:'+ e.pageX+'y:'+e.pageY);
        })
    });
</script>

</body>
</html>
```

> 操作DOM

节点文本操作

```js
$('#text-ul li[name=python]').text();//获得值
$('#text-ul li[name=python]').text('111');//修改值
$('#test-ul').html();//获得值
$('#test-ul').html('<strong>123</strong>');//修改值
```

css的操作

```js
$('#text-ul li[name=python]').css("color","red")
$('#text-ul li[name=python]').css({"color","red"},{...})//多个值
```

元素的显示和隐藏：本质**dispaly：none**；

``` js
$('#text-ul li[name=python]').show()
$('#text-ul li[name=python]').hide()
```

娱乐测试

``` js
$(window).width()
$(window).height()
$('#text-ul li[name=python]').toggle()
```

未来ajax（）：

``` js
$('#from').ajax()
```

> 小技巧
>

1、如何巩固js（看jQuery源码，看游戏源码！）

2、巩固HTML。CSS（扒网站，全部down下来，如何对应修改看效果）



Layer弹窗组件

