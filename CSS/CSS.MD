建议使用这种规范

用link将HTML和CSS连接起来

CSS的优势：

1、内容和表现分离

2、网页结构表现统一，可以实现复用

3、样式十分丰富

4、建议使用独立于html的CSS文件

5、利用SEO，容易被搜索引擎收录

## 1、4 CSS被导入的三种方式

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*内部样式 */
        h1{
            color: #000;
        }
    </style>
    <link rel="stylesheet" href="css2.css">
</head>
<body>
<!--行内样式：在标签元素中，编写一个style属性，编写样式即可-->
<h1 style="color: red">
    我是标题
</h1>
</body>
</html>
```

扩展：外部样式两种写法

- 链接式 html link
- 导入式  CSS2.1 特有的 @import "css2.css";

# 2、选择器

作用：选择页面上的某一个或者某一类元素

## 2.1、基本选择器

1、标签选择器：选择一类标签

2、类选择器 class：选择所有class属性一致的标签，跨标签 .类名{}

3、id选择器：全局唯一！ #id名{}

优先级：id>class>标签

## 2.2、层次选择器

1. 后代选择器 ：在某个元素的后面   
2. 子选择器：一代 儿子
3. 相邻兄弟选择器 同辈
4. 通用选择器

## 2.3、结构伪类选择器

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    避免使用class id选择器-->
    <style>
        /*ul的第一个子元素*/
        ul li:first-child{
            background: #ffc642;
        }
        /*ul的最后一个子元素*/
        ul li:last-child{
            background: #f60c3e;
        }
        /*选中p1：定位到父元素，选择当前的第一个元素
        选择当前p元素的父级元素，选中父级元素的第一个，并且是当前元素才生效
        */
        /*会选择父类下的第二个，当不是p的时候就不会改变*/
        p:nth-child(1){
            background: #1766ff;
        }
        /*会选父类下p类型的第二个,其他的类型不会列入*/
        p:nth-of-type(2){
            background: green;
        }
        a:hover{
            background: gold;
        }
    </style>

</head>
<body>
<a href="">2313213123</a>
<h1>我是h1</h1>
<p>p0</p>
<p>p0</p>
<p>p0</p>
<ul>
    <li>li1</li>
    <li>li2</li>
    <li>li3</li>
</ul>
</body>
</html>
```

## 2.4、属性选择器(常用)

id+class选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .test a{
            float: left;
            display: block;
            height: 50px;
            width: 50px;
            border-radius: 10px;
            background: #0034ff;
            text-align: center;
            color: #c41919;
            text-decoration: none;
            margin-right: 5px;
            font: bold 20px/50px Arial;
        }
        /*属性名,属性名=属性值(正则)*/
        /* = 绝对等于
           *= 包含这个元素
           ^= 以这个开头
           $= 以这个结尾
        */
        /*存在id属性的元素     a[]{}*/
        /*a[id]{*/
        /*    background: yellow;*/
        /*}*/
        /*id=first的元素*/
        /*a[id=first]{*/
        /*    background: yellow;*/
        /*}*/
        /*class中有links的元素*/
        /*a[class*="links"]{*/
        /*    background: yellow;*/
        /*}*/
        /*选中herf属性中以http开头的元素*/
        /*a[href^=http]{*/
        /*    background: yellow;*/
        /*}*/
        a[href$=pdf]{
            background: red;
        }
    </style>
</head>
<body>
<p class="test">
    <a href="https://www.baidu.com/" class="links item first" id="first">1</a>
    <a href="" class="links item active" target="_blank" title="test">2</a>
    <a href="inages/123.png" class="links item" >3</a>
    <a href="inages/123.html" class="links item" >4</a>
    <a href="inages/123.jpg" class="links item" >5</a>
    <a href="abc" class="links item">6</a>
    <a href="/a.pdf" class="links item">7</a>
    <a href="abc.doc" class="links item">8</a>
    <a href="abcd.doc" class="links item first">9</a>
</p>
</body>
</html>
```

```
= 绝对等于
*= 包含这个元素
^= 以这个开头
$= 以这个结尾
```

# 3、美化网页元素

## 3.1、为什么要美化网页

1、有效地传递页面信息

2、美化网页，页面漂亮，才能吸引客户

3、凸显页面的主题

4、提高用户的体验



span标签：重点要突出的字，使用span标签

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #title1{
            font-size: 50px;
        }
    </style>
</head>
<body>
欢迎学习 <span id="title1"> sdd</span>
</body>
</html>
```

## 3.2、字体样式

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--
        font-family：字体 （可以设置两种字体一种英文一种中文）
        font-size:字体大小
        font-weight:字体的粗细
        color:字体的颜色
-->
    <style>
        body{
            font-family: "Arial",微软雅黑;
            color: #c41919;
        }
        h1{
            font-size: 50px;
        }
        .p1{
            font-weight: lighter;
        }
    </style>
</head>
<body>

<h1>故事介绍</h1>

<p>
    dkjskjdlsakjdjsakldlksa dhjshakjfsjdfds
</p>

<p class="p1">
    再喝点水九点半撒娇的啊打扮打扮静安寺不记得把数据库电视剧按计划访客卡
</p>
<p>
    sdjasdhaskjhdaskjhdsjsd
</p>
</body>
</html>
```

## 3.3、文本样式

1、颜色 color rgb rgba

**2、文本对齐的方式 text-align=center**

**3、首行缩进	text-indent**

**4、行高 line-height** 单行文字上下居中！ line-height=height

5、装饰	text-decoration

6、文本图片水平对齐 vertical-align: middle;

## 3.4、阴影

```css
        /*text-shadow:阴影颜色，水平偏移，垂直偏移，阴影半径*/
        #price{
            text-shadow: 10px  10px 10px #1766ff ;
        }
```

## 3.5、超链接伪类

正常情况下，a，a：hover

```css
        /*默认的颜色*/
        a{
            text-decoration: none;
            color: black;
        }
        /*鼠标悬浮的颜色 （只需要记住）*/
        a:hover{
            color: green;
        }
```

## 3.6、列表

```css
/*ul li*/
/*list-style:
    none:去掉原点
    circle：空心圆
    decimal：数字
    square：正方形

*/
ul{
    background: #1e3999;
}
ul li{
    height: 30px;
    list-style: none;
    text-indent: 2em;
}
```

## 3.7、背景

背景颜色

背景图片

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 1000px;
            height: 700px;
            border: 1px solid red;
            background-image: url("images/img.png");
            /*默认是全部平铺的 repeat*/
        }
        /*水平平铺*/
        .div1{
            background-repeat: repeat-x;
        }
        /*垂直平铺*/
        .div2{
            background-repeat: repeat-y;
        }
        /*默认全部平铺*/
        .div3{
            background-repeat: repeat;
        }
        /*不平铺*/
        .div4{
            background-repeat: no-repeat;
        }

    </style>
</head>
<body>
<div class="div1"></div>
<div class="div2"></div>
<div class="div3"></div>
<div class="div4"></div>

</body>
</html>
```

## 3.8、渐变

```css
background-color: #1766ff;
background-image: linear-gradient(19deg,cornflowerblue 0%,crimson 100%) ;
```

# 4、盒子模型

## 4.1、什么是盒子

margin：外边距

padding：内边距

border：边框

## 4.2、边框

1、边框的粗细

2、边框的样式

3、边框的颜色

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*body总有一个默认的外边距margin：0*/
        h1,ul,a,body{
            margin: 0;
            padding: 0;
            text-decoration: none;
        }
        /*border:粗细，样式，颜色*/
        #box{
            width: 300px;
            border: 2px solid red;
            border
        }
        h2 {
            font-size: 16px;
            background-color: #1766ff;
            line-height: 30px;
            /*margin: 0;*/
            color: white;
        }
        form{
            background: #0034ff;
        }
        div:nth-of-type(1) input{
            border: 3px solid black;
        }
        div:nth-of-type(2) input{
            border: 3px dashed #53a34e;
        }
        div:nth-of-type(3) input{
            border: 3px dashed #53a34e;
        }
    </style>
</head>
<body>
<div id="box">
    <h2>会员登入</h2>
    <form action="#">
        <div>
            <span>姓名：</span>
            <input type="text">
        </div>
        <div>
            <span>密码：</span>
            <input type="text">
        </div>
        <div>
            <span>邮箱：</span>
            <input type="text">
        </div>

    </form>
</div>
</body>
</html>
```

## 4.3、内外边距

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    外边距的妙用：居中元素
-->
    <style>
        #boxz{
            width: 300px;
            border: 2px solid red;
            margin: 0 auto;
        }
        /*
        顺时针选择
        margin:0
        margin:0 1px
        margin:0 1px 2px 3px
        */
        h2 {
            font-size: 16px;
            background-color: #1766ff;
            line-height: 30px;
            /*margin: 0;*/
            color: white;
            margin: 0 1px;
        }
        form{
            background: #0034ff;
        }
        input{
            border: 1px solid black;
        }
    </style>
</head>
<body>
<div id="box">
    <h2>会员登入</h2>
    <form action="#">
        <div>
            <span>姓名：</span>
            <input type="text">
        </div>
        <div>
            <span>密码：</span>
            <input type="text">
        </div>
        <div>
            <span>邮箱：</span>
            <input type="text">
        </div>

    </form>
</div>
</body>
</html>
```

盒子的计算方式：你这个元素到底多大？

![image-20210322000608254](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210322000608254.png)

margin+border+padding+内容的宽度

## 4.4、圆角边框

四个角

```html
width: 100px;
height: 100px;
border: 10px solid red;
border-radius: 50px 20px 10px 10px;
```

## 4.5、盒子阴影

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*div{*/
        /*    width: 50px;*/
        /*    height: 100px;*/
        /*    border: 10px solid red;*/
        /*    box-shadow: 10px 10px 100px yellow;*/
        /*}*/
        /*
        margin: 0 auto;居中
        要求：块元素，块元素有固定的宽度
        */
        img{
            border-radius: 50px;
            box-shadow: 10px 10px 100px yellow;
        }
    </style>
</head>
<body>
<div style="width: 500px;display: block;text-align: center">
        <img src="images/img.png" alt="">
</div>

</body>
</html>
```

# 5、浮动

## 5.1、标准文档流

![image-20210324111110904](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210324111110904.png)

块级元素：独占一行

``` 
h1~h6 p div 列表....
```

行内元素：不独占一行

``` 
span a img strong...
```

行内元素可以被包含在块级元素中，反之，则不可以

## 5.2、display

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
    block 块元素
    inline行内元素
    inline-block   是块元素，但是可以内联，在一行     保持块元素的特性，但是能写成一行
    none
    -->
    <style>
        div{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            display: inline;
        }
        span{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            /*inline-block既是行内元素，又是块元素*/
            display: inline-block;
        }
    </style>
</head>
<body>
<div>div块元素</div>
<span>span行内元素</span>
</body>
</html>
```

1、这个也是一种实现行内元素排列的方式，但是我们很多情况都是用float

## 5.3、float

1、左右浮动 float

```css
div{
    margin: 10px;
    padding: 5px;
}
#father{
    border: 1px #7700ff solid;
}
.layer01{
    border: 1px #00ff2a dashed;
    display: inline-block;
    float: left;
}
.layer02{
    border: 1px #ff9900 dashed;
    display: inline-block;
    float: left;
}
.layer03{
    border: 1px #8000ff dashed;
    display: inline-block;
    float: right;
}
.layer04{
    border: 1px #00ffff dashed;
    display: inline-block;
    float: left;
   
}
```

## 5.4、父级边框塌陷的问题

clear

```css
clear：right；右侧不允许有浮动元素
clear：left； 左侧不允许有浮动元素
clear：both； 两侧不允许有浮动元素
clear：none；
```

解决方案：

1、增加父级元素的高度~

```css
#father{
    border: 1px #7700ff solid;
    height: 800px;
}
```

2、增加一个空的div，清除浮动

```css
<div class="clear"></div>
```

```css
.clear{
    clear: both;
    margin: 0px;
    padding: 0;
}
```

3、overflow

在父级元素中增加一个overflow：hidden；

4、父类增加一个伪类：after

```css
#father:after{
    content: "";
    display: block;
    clear: both;
}
```

**小结：**

1.浮动元素后面增加空的div

​	简单，空的div是不好的，代码中尽量避免

2.设置父元素的高度

​	简单，元素假设有了固定的高度，就会被限制

3.overflow

​	简单，下拉的一些场景避免使用

4.父类添加一个伪类：after（推荐）

​	写法稍微复杂一点，但是没有副作用，推荐使用！

## 5.5、对比

**display**

方向不可以控制

**float**

浮动起来的话会脱离标准文档流，所以要解决父级边框塌陷的问题

# 6、定位

## 6.1、相对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--    相对定位
    相对于自己原来的位置进行偏移
    -->
    <style>
        body{
            padding: 20px;
        }
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: 1px solid #666;
            padding: 0;
        }
        #first{
            background-color: #e5ff84;
            border: 1px dashed #c21616;
            position: relative;
            /*相对定位：上下左右*/
            top : -20px;
            left: 20px;
        }
        #second{
            background-color: #3dc499;
            border: 1px dashed #3dc458;
            position: relative;
            bottom: -10px;
        }
        #third{
            background-color: #232a99;
            border: 1px dashed #232aa3;
            position: relative;
            bottom: -10px;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```

相对定位：position: relative;

相对于原来的位置，进行指定的偏移，相对定位的话，它任然在标准文档流中，原来的位置会被保留。

## 6.2、绝对定位

定位：基于XXX定位，上下左右

1、没有父级元素定位的前提下，就是相对于浏览器 【没有#father{position: relative;}子元素的position: absolute;就是相对于浏览器】

2、假设父级元素存在定位，我们通常会相对于父级元素进行偏移。（一般使用这个）

3、在父级元素范围内移动

相对于父级或者浏览器的位置，进行指定的偏移，绝对定位的话，它不在标准文档流中，原来的位置不会被保留。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: 1px solid #666;
            padding: 0;
            position: relative;
        }
        #first{
            background-color: #e5ff84;
            border: 1px dashed #c21616;
        }
        #second{
            background-color: #3dc499;
            border: 1px dashed #3dc458;
            position: absolute;
            right: 30px;
        }
        #third{
            background-color: #232a99;
            border: 1px dashed #232aa3;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```

## 6.3、固定定位fixed

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body{
            height: 1000px;
        }
        /*绝对定位：相对于浏览器*/
        div:nth-of-type(1){
            width: 100px;
            height: 100px;
            background: red;
            position: absolute;
            right: 0px;
            bottom: 0px;
        }
        div:nth-of-type(2){
            width: 50px;
            height: 50px;
            background: yellow;
            position: fixed;
            right: 0px;
            bottom: 0px;
        }
    </style>

</head>
<body>

<div>div1</div>
<div>div2</div>

</body>
</html>
```

## 6.4、z-index

图层~

z-index：默认是0，最高是无限999

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="CSS/style.css">
</head>
<body>
<div id="content">
    <ul>
        <li><img src="images/img_1.png" alt=""></li>
        <li class="tipText">sdasdsdsdsdas</li>
        <li class="tipBg">s</li>
        <li>时间：2099-01-01</li>
        <li>地点：月球一号基地</li>
    </ul>
</div>
</body>
</html>
```

opacity：0.5；/背景透明度/

```css
#content{
    width: 380px;
    padding: 0px;
    margin: 0px;
    overflow: hidden;
    font-size: 12px;
    line-height: 25px;
    border: 1px #000 solid;
}
ul,li{
    padding: 0px;
    margin: 0px;
    list-style: none;
}
/*父级元素相对定位*/
#content ul{
    position: relative;
}
.tipText,.tipBg{
    position: absolute;
    width: 380px;
    height: 25px;
    top: -10px;
}
.tipText{
    color: white;
    /*z-index: 999;*/
}
.tipBg{
    background: #000;
    /*背景透明度*/
    opacity: 0.5;
}
```

# 7、动画

# 8、总结

