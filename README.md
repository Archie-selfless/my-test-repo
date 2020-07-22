# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>

# CSS布局
## 双飞翼
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="x-ua-compatible" content="ie=egde">
    <title>Demo003</title>
    <style>
        .left, .right, .main{
            min-height: 200px;
            float: left;
        }
        .left {
            width: 200px;
            background-color: #2a6495;
            margin-left: -100%;
        }
        .main{
            color: #FFF;
            width: 100%;
            background-color: #000;
        }
        .right {
            width: 300px;
            background-color: #2a5b52;
            margin-left: -300px;
        }
        .main-inner {
            margin-left: 200px;
            margin-right: 300px;
        }
    </style>
</head>
<body>
<div class="main">
    <div class="main-inner">中心区</div>
</div>
<div class="left">左翼</div>
<div class="right">右翼</div>
</body>
</html>
```

## 四类定位
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="x-ua-compatible" content="ie=egde">
    <title>Demo003</title>
    <style type="text/css">
        p {
            font-size: 11pt;
            color: #363636;
            text-indent: 2em;
        }

        .parent {
            width: 500px;
            height: 150px;
            margin-top: 20px;
            margin-left: 20px;
            border: solid 1px #555555;
            background: #aaaaaa;
        }

        .parent div {
            width: 100px;
            height: 80px;
            float: left;
            background: #708090;
            border: dashed 1px #008B8B;
            font-size: 12pt;
            font-weight: bold;
            color: #104E8B;
        }
    </style>
</head>
<body>
<!--相对定位!-->
<h2>relative</h2>
<p>相对定位是一个非常容易掌握的概念。如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动。</p>
<div class="parent">
    <div>child 1</div>
    <div style="position:relative;left:20px;top:20px;">child 2</div>
    <div>child 3</div>
</div>

<!--绝对定位!-->
<h2>absolute</h2>
<p>绝对定位的元素的位置相对于最近的已定位祖先元素，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块。
    对于定位的主要问题是要记住每种定位的意义。</p>
<p>绝对定位是“相对于”最近的已定位祖先元素，如果不存在已定位的祖先元素，那么“相对于”最初的包含块。所以如果要设定元素与其父元素的绝对位置定位就必须设定父元素的定位。</p>
<p>注释：根据用户代理的不同，最初的包含块可能是画布或 HTML 元素。</p>
<div class="parent" style="position:relative;"<!--如果该处不定位，那么child5框的定位是相对于最初的包含块!-->>
<div>child 4</div>
<div style="position:absolute;left:20px;top:20px;">child 5</div>
<div>child 6</div>
</div>

<!--相对定位!-->
<h2>fixed</h2>
<p>元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。</p>
<div class="parent">
    <div>child 7</div>
    <div style="position:fixed;right:20px;top:20px;">child 8</div>
    <div>child 9</div>
</div>

<!--相对定位!-->
<h2>static</h2>
<p>元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。</p>
<div class="parent">
    <div>child 10</div>
    <div style="position:static;right:20px;top:20px;">child 11</div>
    <div>child 12</div>
</div>
</body>
```

## 经典层叠
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo004</title>
    <style>
        body {
            padding: 100px;
        }
        div{
            width: 200px;
            height: 200px;
            float: left;
        }
        .first {
            background-color: #2a5b52;
            position: relative;
            z-index: -2;
        }
        .second {
            background-color: #2a6495;
            position: absolute;
            left: 120px;
            top: 150px;
            z-index: -1;
        }
        .third {
            float: none;
            background-color: #1ABC9C;
            margin-left: 40px;
            margin-top: 90px;
        }
        .fourth {
            background-color: #4d4d4d;
            margin-left: 70px;
            margin-top: -150px;
        }
        .fifth {
            background-color: #2e0d0e;
            display: inline-block;
            margin-left: -170px;
            margin-top: -110px;
        }
        .sixth {
            background-color: #010101;
            margin-left: -150px;
            margin-top: -70px;
        }
    </style>
</head>
<body>

<div class="first"></div>
<div class="second"></div>
<div class="third"></div>
<div class="fourth"></div>
<div class="fifth"></div>
<div class="sixth"></div>
<p style="position: fixed; bottom: 10px;">负z-index(-2) < 负z-index(-1) < 常规流块级元素&非position后代 < 浮动盒&非position后代 < inline盒子&非position后代 < z-index升序</p>
</body>
</html>
```

## 解决inline-box间隙问题
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo005</title>
    <style>
        span{
            background-color: #2a6495;
        }
        .method2 span {
            font-size: 17px;
        }
    </style>
</head>
<body>
<H4>inline-box的间隙</H4>
<div class="origin">
    <span>111</span>
    <span>222</span>
    <span>333</span>
    <span>444</span>
</div>
<h4>解决方式1：删除换行符（IE像素残留）</h4>
<div class="method1">
    <span>111</span><span>222</span><span>333</span><span>444</span>
</div>
<h4>解决方式2：父元素 设置font-size：0 ；letter-spacing：-3px (Chrom浏览器不需要)，子元素重新设置font-size</h4>
<div class="method2" style="font-size: 0;">
    <span>111</span>
    <span>222</span>
    <span>333</span>
    <span>444</span>
</div>
</body>
</html>
```

****

## 基于视口垂直居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基于视口垂直居中</title>
    <style>
        .wrapper {
            background-color: #2a6495;
            width: 1000px;
            height: 800px;
            overflow: hidden;
        }
        .center {
            width: 18em;
            height: 10em;
            text-align: center;
            background-color: #2a5b52;
            color: #FFF;
            /* 1vh = 1% * 视口高度 */
            margin: 50vh auto;
            transform: translateY(-50%);
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        基于视口 <br>
        不要求原生有固定高度 <br>
        只基于窗口，不基于父元素 <br>
    </div>
</div>
</body>
</html>
```
## 定宽垂直居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定宽居中</title>
    <style>
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            text-align: center;
            color: #FFF;

            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -9em;
            margin-top: -5em;
        }
    </style>
</head>
<body>
<div class="center">
    要求原生有固定的宽高。<br/>
    position: absolute;<br/>
    top和left 为 50%;<br/>
    margin上为高的一半<br/>
    margin左为宽的一半<br/>
</div>
</body>
</html>
```

# calc垂直居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定宽居中</title>
    <style>
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            text-align: center;
            color: #FFF;

            position: absolute;
            top: calc(50% - 5em);
            left: calc(50% - 9em);
        }
    </style>
</head>
<body>
<div class="center">
    要求原生有固定的宽高。<br/>
    position: absolute;<br/>
    top 为 calc(50% 剪 一半高)
    left 为 calc(50% 剪 一半宽)
</div>
</body>
</html>
```

## transform垂直居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定宽居中</title>
    <style>
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            text-align: center;
            color: #FFF;

            position: absolute;
            top: 50%;
            left: 50%;
            transform : translate(-50%, -50%);
        }
    </style>
</head>
<body>
<div class="center">
    要求原生有固定的宽高。<br/>
    position: absolute;<br/>
    top和left 为 50%;<br/>
    transform: translate(-50%, -50%);
</div>
</body>
</html>
```

## flex垂直居中方法1
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>flex居中1</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;
            display: flex;
        }
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            text-align: center;
            color: #FFF;

            margin: auto;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        使用flex居中 <br>
        父元素 display : flex <br>
        居中块 margin ： auto
    </div>
</div>
</body>
</html>
```


## flex垂直居中方法2
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>flex居中1</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;

            display: flex;
            /* 盒子横轴的对齐方式 */
            justify-content: center;
            /* 盒子纵轴的对齐方式 */
            align-items: center;
        }
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            text-align: center;
            color: #FFF;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        使用flex居中<br/>
        父元素 display: flex; <br/>
        justify-content: center;<br/>
        align-items: center;<br/>
    </div>
</div>
</body>
</html>
```

## text-align的center属性水平居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>flex居中1</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;
            text-align: center;
        }
        .center {
            display: inline-block;
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            color: #FFF;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        如果需要居中的元素为常规流中 inline / inline-block 元素，为父元素设置 text-align: center;
    </div>
</div>
</body>
</html>
```

## margin的auto属性 水平居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>水平居中</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;
            text-align: center;
        }
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            color: #FFF;

            margin: 0 auto;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        如果需要居中的元素为常规流中 inline / inline-block 元素，为父元素设置 text-align: center;
    </div>
</div>
</body>
</html>
```

## 绝对定位水平居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>水平居中</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;
            position: relative;
        }
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            color: #FFF;
            position: absolute;
            left: 50%;
            margin-left: -9em;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        如果元素positon: absolute; 那么 <br>
        0）设置父元素postion: relative <br>
        1）为元素设置宽度，<br>
        2）偏移量设置为 50%，<br>
        3）偏移方向外边距设置为元素宽度一半乘以-1
    </div>
</div>
</body>
</html>
```

## 相对定位水平居中
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>水平居中</title>
    <style>
        .wrapper {
            width: 1000px;
            height: 600px;
            background-color: #2a6495;
        }
        .center {
            width: 18em;
            height: 10em;
            background-color: #2a5b52;
            color: #FFF;
            position: relative;
            left: 50%;
            margin-left: -9em;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="center">
        如果元素positon: relative; 那么 <br>
        0）为元素设置宽度 <br>
        1）偏移量设置为 50%，<br>
        2）偏移方向外边距设置为元素宽度一半乘以-1，<br>
    </div>
</div>
</body>
</html>
```

****
# CSS效果
## 使用div绘制图形（三角形）——进阶可以学习clip-path的用法画各种图形！
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>绘制图形</title>
    <style>
        .triangles {
            width: 0;
            height: 0;
            border-left: 100px solid red;
            border-top: 100px solid blue;
            border-bottom: 100px solid green;
            border-right: 100px solid yellow;
        }
    </style>
</head>
<body>
<div class="triangles"></div>
</body>
</html>
```

# 实现0.5px的边框
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>绘制图形</title>
    <style>
        .custom-border{
            width:200px;
            margin:10px auto;
            height:100px;
            border:1px solid #333;
            background-color:#eee;
            padding:10px;
        }
        .scale-border{
            margin:10px auto;
            height:100px;
            position:relative;
            padding:10px;
            width: 200px;
        }
        .content{
            position:relative;
            z-index:2;
        }
        .border{
            transform:scale(0.5); /* 通过整体缩放使得边界变为0.5px */
            position:absolute;
            border:1px solid #333;
            top:-50%;
            right:-50%;
            bottom:-50%;
            left:-50%;
            background-color:#eee;
        }
    </style>
</head>
<body>
<div class="custom-border border-color">边框宽度1px</div>
<div class="scale-border">
    <div class="content">边框宽度0.5px</div>
    <div class="border border-color"></div>
</div>
</body>
</html>
```

# 实现3D效果（旋转的硬币）
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>3D效果</title>
    <style>
        .box {
            position: relative;
            height: 200px;
            width: 200px;
            margin: 200px auto;
            transition: all 1s;
            transform-style: preserve-3d; /* 保留子元素的3d空间，这个是给父盒子添加的！ */
            transform: perspective(500px); /* 透视，用在要动的元素上 */
        }
        /* 用定位将两个盒子叠加在一起 */
        .coin-front, .coin-back {
            position: absolute;
            height: 200px;
            width: 200px;
            border-radius: 50%;
            color: #fff;
            text-align: center;
            line-height: 200px;
        }
        .coin-front {
            background-color: #1F2438;
            z-index: 1; /* 提高硬币正面的z轴 */
        }
        .coin-back {
            background-color: #000;
            transform: rotateY(180deg); /*沿y轴3d旋转180度，旋转以后，两个盒子就实现背靠背了，这样文字就不会镜像*/
        }
        .box:hover {
            transform: rotateY(180deg);
        }
    </style>
</head>
<body>
<div class="box">
    <div class="coin-front">水可载舟</div>
    <div class="coin-back">亦可覆舟</div>
</div>
</body>
</html>
```

# 响应式布局(JS模拟)
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>test</title>
    <style>
        .container {
            margin:auto;
            height: 40px;
            background-color: #2a5b52;
        }
    </style>
</head>
<body>
<div class="container">
    <p id="dynamic-width" style="color: white"></p>
</div>

<script>
    window.addEventListener("load", function () {
        // 1. 获取容器
        let container = document.querySelector(".container");
        let dynamic_width = document.getElementById("dynamic-width");
        let clientw = 0;
        resize();
        // 2. 监听窗口的大小变化
        window.addEventListener("resize", resize);
        function resize() {
            // 2.1 获取改变后的宽度
            clientw = window.innerWidth;
            // 2.2 根据宽度转变容器大小
            if (clientw >= 1200) { // 超大屏幕
                container.style.width = "1170px";
            }else if (clientw >= 992) { // 大屏幕
                container.style.width = "970px";
            }else if (clientw >= 768) { // 小屏幕
                container.style.width = "750px";
            }else { // 超小屏幕
                container.style.width = "100%";
            }
            dynamic_width.innerText = 'width:' + container.style.width;
        }
    })
</script>

</body>
</html>
```

# 响应式布局（CSS实现）
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>test</title>
    <style>
        .container {
            margin: auto;
            height: 40px;
            background-color: #2a5b52;
        }

        /* 媒体查询 */
        @media screen and (max-width: 768px) {
            .container {
                width: 100%;
            }
        }

        @media screen and (min-width: 768px) and (max-width: 992px) {
            .container {
                width: 750px;
            }
        }

        @media screen and (min-width: 992px) and (max-width: 1200px) {
            .container {
                width: 970px;
            }
        }

        @media screen and (min-width: 1200px) {
            .container {
                width: 1170px;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <p id="dynamic-width" style="color: white"></p>
</div>
</body>
</html>
```

## PostCSS的实现原理
### PostCSS是一个通过JS插件转换样式表的工具，它本身并不是一门新的CSS语言，而是一个平台或者是生态心态，提供插件扩展服务即JS API，开发者可以根据这些接口，定制开发插件， 目前比较流行的插件工具如：Autoprefixer 、Stylelint 、CSSnano

***
# JS基础
## typeof可以及检测的数据类型有哪些
* 基本数据类型：Undefined null bool string number
* 关键点：typeof只能区分值类型，不能区分引用类型
* JS中的基本数据类型：null, undefined, bool, string, number（typeof可以区分除了null以外的四种值类型）
* typeof 6种类型：Object({},[],null), Undefined, Boolean, Number, Function, String
* typeof可以区分值类型，typeof null = Object

## JS中===和==的区别
### 区别：
== 会进行强制类型转换之后再比较，=== 不会进行强制类型转换的
### 应用场景：
1. （用于判断对象属性是否存在）：if (obj == null) ===>>> 等价于if (obj == null || obj == undefined),可以简化代码，其他情形都使用===进行比较
2. 用于判断函数的参数是否存在： function(a, b){ if(a == null) { // ... }}
3. 对于函数内部或者是一个对象的参数进行判断只会出现undefined， 而不会报错（慎用）
### js中类型转换为false的有哪些(6种)
null, undefined, NaN, '', false, 0

## JS中的内置函数有哪些
* 内置函数： Object Array Boolean Number String Function Date RegExp Error
* 内置对象：Math, JSON

## 原型和原型链
### 原型链的5条规则
1. 所有的引用类型（数组，对象，函数），都是具有对象特性的，即可以自由扩展属性（除了null以外）
2. 所有的引用类型（数组、对象、函数），都有一个proto 属性（隐式原型），这个属性的值是一个普通对象
3. 所有的函数，都有一个prototype属性（显式原型），这个属性值是一个普通的对象
4. 有的引用类型（数组、对象、函数），proto的属性值指向（完全相等）它的构造函数的“prototype”的属性值
5. 试图得到一个对象的某一个属性的时候，如果一个对象本身没有这个属性的话，就会去它的proto( 也就是它的构造函数中去寻找这个属性)

### instanceof的作用
判断【引用类型】属于哪个【构造函数】的方法

### 写一个原型继承的例子
### 描述一下new一个对象的过程

## 作用域和闭包
### 函数表达式和函数声明的区别
1. 函数声明中函数名是必须的，函数表达式中则是可选的。
2. 用函数声明定义的函数，函数可以在函数声明之前调用，而用函数表达式定义的函数则只能在声明之后调用。

### 对执行上下文（ECStack）的理解
#### 执行上下文可以理解为当前代码的执行环境，它会形成一个作用域。JavaScript中的运行环境大概包括三种情况
1. 全局环境：JavaScript代码运行起来会首先进入的环境
2. 函数环境：当函数被调用执行时，会进入被调用的函数中执行代码
3. eval（不推荐使用会对JS的执行效率产生影响）
（JavaScript引擎会以栈的方式来处理它们，这个栈，我们称其为函数调用栈(call stack)。栈底永远都是全局上下文，而栈顶就是当前正在执行的上下文。）

### 对this的理解
1. 作为构造函数执行
2. 作为对象属性执行
3. 作为普通函数执行
4. call apply bind

### 严格模式下的this
### 箭头函数中的this
### call,apply,bind的区别
### JS中作用域的理解
### 什么是自由变量和作用域链
### 闭包的使用场景
1. 函数作为返回值
  1. 一个函数的返回值是一个函数，父级作用域是指，定义时候的作用域，而不是执行的作用域
2. 函数作为参数传递
  2. 【重点】：函数作用域中的自由变量会在声明的父级作用域中去寻找，而不是去执行的时候的作用域中去寻找变量
### 创建10个a标签，点击的时候，弹出对应的序号
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>test</title>
</head>
<body>
</body>

<script>
    createHrefElements();

    // 使用立即函数+闭包实现的
    function createHrefElementsTwo() {
        for (var i = 0; i < 10; i++) {
            // 一个函数就是一个作用域，这里相当于是创建了10个函数作用域，每一个作用域里面都是有自己的一歌变量i的，这是当用户需要这个自由变量的时候，
            // 就会直接去这个这个函数作用域范围内寻找这个变量，每一个里面就是一个单独的函数作用域
            (function (i) {
                // 这里面的就是单独的一个函数作用域
                var a = document.createElement('a');
                a.innerText = '我是立即函数中的' + i;
                a.href = '#';
                a.addEventListener('click', function (e) {
                    e.preventDefault(); // 禁止掉浏览器的默认事件,只让浏览器执行我们规定的函数.
                    // 分析：由这个for循环可以发现，这个i实际上是一个函数作用域的变量，这个i一直是变化的，当i等于9的时候，创建完毕最后一个元素，
                    // 最后执行完毕i++, i的最终结果就是10，因此对于每一个a标签点击都是一个10
                    alert(i);                   // 这里的i最后可以实现点击就弹出对应的编号吗？
                });
                document.body.appendChild(a);
                document.body.appendChild(document.createElement('br'));
            })(i);      //  这里的i和这个里面的状态信息保持一致的
        }
    }
</script>

</html>
```
### 函数curry化
#### 定义
柯里化函数(curried function)每次返回一个一元函数: 每次携带一个参数的函数
#### 实现
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>test</title>
</head>
<body>
</body>
<script>
    console.log(add(1,2,3)(1)(2)(3)(4,5,6)(7,8)());

    function add() {
        /* curry化实现（例- add(1,2,3)(1)(2)(3)(4,5,6)(7,8)() === 42） */
        let test = [];
        test = [].slice.call(arguments);
        /* 从下方开始有点类似于递归，把每个要加入的 参数式子 都当做一个整体进行处理 */
        return function () {
            let args = [].slice.call(arguments), len = args.length;
            if (len !== 0) { // 若后续还有参数，则继续加入数组中
                test = test.concat(args);
                return arguments.callee;
            } else {
               return test.reduce((a,b) => {return a + b;});
            }
        }
    }
</script>
</html>
```

### 实现一个bind函数
```

```
### 前端使用异步的场景
### 实现一个自己的ajax
### 获取 YYYY-MM-DD 格式的日期
### 获取一个长度一致的随机字符串
### 一个能遍历对象和数组通用的forEach函数
### 手动编写一个ajax，不依赖第三方库
### 跨域的几种实现方式以及底层的实现原理

***
## 运行环境
### 浏览器渲染页面的过程
1. 根据HTML结构生成DOM Tree（单个节点，没样式）
2. 根据CSS生成CSSOM（CSS对象模型）
3. 将DOM和CSSOM整合生成一个RenderTree（每个节点都有自己的样式）
4. 根据RenderTree开始渲染和显示
5. 遇到script标签的时候，会执行并阻塞渲染（渲染权交给了js）----JS加载完毕之后然后执行代码
### 懒加载和预加载的区别和实现原理
### 前端性能优化的方法有哪些
### 重绘和回流的区别
* 重绘：当render tree中的一些元素需要更新属性（只影响元素外观、风格，不影响布局）
* 回流：当render tree中的一部分因为元素的尺寸、布局、隐藏等盖面需要重新构建（页面布局和集合属性改变）
### XSS攻击
利用用户的cookie进行恶意欺骗（cookie发送到外部服务器）(标签转义、白名单、黑名单过滤)
### CSRF攻击
论坛发送了一个删帖的API链接（图片），结果删除了自己的帖子。[恶意发帖、删帖]（验证码、token）
#### 二者区别
XSS是获取信息，不需要提前知道其他用户页面的代码和数据包。
CSRF是代替用户完成指定的动作，需要知道其他用户页面的代码和数据包
### ES6中常用的功能
1. let/const
2. 多行字符串/模板变量
3. 解构赋值
4. 块级作用域？【重点理解】
5. 函数默认参数
6. 箭头函数（this指向问题）
#### var、let 及 const 区别
* var声明的变量会挂载在window上，而let和const不会
* var声明变量存在变量提升，let和const不会
* let、const 的作用范围是块级作用域，而var的作用范围是函数作用域
* 同一作用域下let和const不能声明同名变量，而var可以
* 同一作用域下在let和const声明前使用会存在暂时性死区
* const
  * 一旦声明必须赋值,不能使用null占位
  * 声明后不能再修改
  * 如果声明的是复合类型数据，可以修改其属性
#### Proxy
#### 数组方法
#### Es6中箭头函数与普通函数的区别
* 普通function的声明在变量提升中是最高的，箭头函数没有函数提升（箭头函数没有原型属性）
* 箭头函数没有属于自己的this、arguments
* 箭头函数不能作为构造函数，不能被new，没有property
* call和apply方法只有参数，没有作用域
* 箭头函数的this永远指向其上下文的 this，任何方法都改变不了其指向，如call(), bind(), apply(),普通函数的this指向调用它的那个对象
#### Promise
Promise 翻译过来就是承诺的意思，这个承诺会在未来有一个确切的答复，并且该承诺有三种状态，这个承诺一旦从等待状态变成为其他状态就永远不能更改状态了。
* 等待中（pending）
* 完成了（resolved）
* 拒绝了（rejected）
当我们在构造 Promise 的时候，构造函数内部的代码是立即执行的.
Promise 实现了链式调用，也就是说每次调用 then 之后返回的都是一个 Promise，并且是一个全新的 Promise，原因也是因为状态不可变。如果你在 then 中 使用了 return，那么 return 的值会被 Promise.resolve() 包装。
Promise 也很好地解决了回调地狱的问题
它也是存在一些缺点的，比如无法取消 Promise，错误需要通过回调函数捕获
#### async 和 await
一个函数如果加上 async ，那么该函数就会返回一个 Promise
async 就是将函数返回值使用 Promise.resolve() 包裹了下，和 then 中处理返回值一样，并且 await 只能配套 async 使用
async 和 await 可以说是异步终极解决方案了，相比直接使用 Promise 来说，优势在于处理 then 的调用链，能够更清晰准确的写出代码，毕竟写一大堆 then 也很恶心，并且也能优雅地解决回调地狱问题
也存在一些缺点，因为 await 将异步代码改造成了同步代码，如果多个异步代码没有依赖性却使用了 await 会导致性能上的降低
#### Generator 生成器
```
function *foo(x) {
  let y = 2 * (yield (x + 1))
  let z = yield (y / 3)
  return (x + y + z)
}
let it = foo(5)
console.log(it.next())   // => {value: 6, done: false}
console.log(it.next(12)) // => {value: 8, done: false}
console.log(it.next(13)) // => {value: 42, done: true}
```
* Generator 函数调用和普通函数不同，它会返回一个迭代器
* 当执行第一次 next 时，传参会被忽略，并且函数暂停在 yield (x + 1) 处，所以返回 5 + 1 = 6
* 当执行第二次 next 时，传入的参数等于上一个 yield 的返回值，如果你不传参，yield 永远返回 undefined。此时 let y = 2 12，所以第二个 yield 等于 2 12 / 3 = 8
* 当执行第三次 next 时，传入的参数会传递给 z，所以 z = 13, x = 5, y = 24，相加等于 42
#### 生成器原理
当yeild产生一个值后，生成器的执行上下文就会从栈中弹出。但由于迭代器一直保持着队执行上下文的引用，上下文不会丢失，不会像普通函数一样执行完后上下文就被销毁

***
## MVVM和VUE
### v-bind和v-model的区别
1. v-bind用来绑定数据和属性以及表达式，缩写为'：'
2. v-model使用在表单中，实现双向数据绑定的，在表单元素外使用不起作用
### Vue 中三要素
#### 响应式
* 修改 data 属性之后， vue 立刻监听
* data 属性被代理到 vm 上
#### 模板引擎
```
    <div id="app">
        <div>
            <input v-model="title">
            <button v-on:click="add">submit</button>
        </div>
        <ul>
            <li v-for="item in list"></li>
        </ul>
    </div>
```
* 本质：字符串
* 有逻辑（v-if\v-for）
* 最终还是要转换成html显示
* 最终必须要转换成js代码，因为：
  1. 逻辑性必须由js实现（图灵完备）
  2. html的页面渲染是静态的，必须通过js注入灵魂
#### 渲染
```
var obj = {
    name: 'zhangsan',
    age: 20,
    getAddress(){
        alert('shanghai');
    }
}

// 不使用with
function fn() {
  alert(obj.name);
  alert(obj.age);
  obj.getAddress();
}

// 使用with(代码不易维护！！！)
function fn1() {
  with(obj){
      alert(name);
      alert(age);
      getAddress();
  }
}

fn();
fn1();
```
### vue 的整个实现流程
* 第一步: 解析模板成 render　函数
* 第二步: 响应式开始监听
* 第三步: 首次渲染，显示页面，且绑定依赖
* 第四步: data 属性变化，触发 render

### vm的实质
vm负责让数据变了，视图能自动发生变化。背后的原理是Object.defineProperty。
其实就是属性的读取和设置操作都进行了监听，当有这样的操作的时候，进行某种动作。

### vue 的双向绑定的原理
* vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
1. 需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化
2. compile 解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
3. Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要做的事情是:
  * 在自身实例化时往属性订阅器(dep)里面添加自己
  * 自身必须有一个 update()方法
  * 待属性变动 dep.notice()通知时，能调用自身的 update() 方法，并触发 Compile 中绑定的回调，则功成身退。
4. MVVM 作为数据绑定的入口，整合 Observer、Compile 和 Watcher 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用 Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据 model 变更的双向绑定效果
* (绑定所有属性避免后期加新属性。如果是数组，只能通过数组方法修改数组。如下例子，控制台vm.arr--发现视图并不会变化，vm.arr.push(4)就能变化)
```
        <script src="node_modules/vue/dist/vue.js"></script>
        <script>
        let vm = new Vue({
            el:'#app',
            // template加上之后会替换掉#app这个标签
            // template:'<h1>en</h1>',
            data:{msg:'msg',arr:[1,2,3]}
        })
        vm.msg = 'msg'
        </script>
```
### vue 的优点和缺点是什么
#### 优点
1. 低耦合。视图（View）可以独立于 Model 变化和修改，一个 ViewModel 可以绑定到不同的"View"上，当 View 变化的时候 Model 可以不变，当 Model 变化的时候 View 也可以不变。
2. 可重用性。你可以把一些视图逻辑放在一个 ViewModel 里面，让很多 view 重用这段视图逻辑。
3. 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用 Expression Blend 可以很容易设计界面并生成 xml 代码。
4. 可测试。界面素来是比较难于测试的，而现在测试可以针对 ViewModel 来写
#### 缺点
1. 网站SEO问题
2. 浏览器兼容性问题
3. 海量数据节点的渲染问题

### vue 生命周期
* 8个阶段：创建前/后，载入前/后，更新前/后，销毁前/后
1. 创建前/后： 在 beforeCreate 阶段，vue 实例的挂载元素 el 还没有, created阶段。
2. 载入前/后：在 beforeMount 阶段，vue 实例的$el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点，data.message 还未替换。在 mounted 阶段，vue 实例挂载完成，data.message 成功渲染。
3. 更新前/后：当 data 变化时，会触发beforeUpdate 和 updated方法。
4. 销毁前/后：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 的绑定，但是 dom 结构依然存在
### Vue组件之间的传值
### Vue路由
### Vue指令
### Vux
### axios
***
# JS原型
***
# JS异步
***
# JS正则
***
# JS函数
***
# NodeJS
***
# 性能优化
***
# Webpack
***
# Web安全
***
# 计算机网络
***
# 操作系统
***
# 数据结构
***
# 开发环境
***
# 编程题







# 个人主页
## HTML
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial=1.0">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <title>test</title>
    <link rel="stylesheet" href="test.css">
</head>
<body>
<nav id="navbar">
    <ul>
        <li><a href="./test.html" name="Home">主页</a></li>
        <li><a href="#" name="Portfolio">作品集</a></li>
        <li><a href="#" name="Blog">博客</a></li>
        <li><a href="#" name="Contaction">联系我</a></li>
    </ul>
</nav>

<header>
    <div class="function-area">
        <button id="back-home" class="back-home">Back Home</button>
        <span><a href="#">My GitHub</a></span>
    </div>
    <h1>Archie's Technical Blog</h1>
    <p><strong>Tec attack</strong> save the world</p>

</header>

<div class="container">
    <div class="infomation">
        aaa...
    </div>
</div>

<div class="footer" style="text-align: center">博主信息
    <span>电话</span>
    <span>居住地</span>
    <span>邮箱</span>
</div>

</body>
</html>
```

## CSS
```
body {
    position: absolute;
    height: 100%;
    left: 10px;
    right: 10px;
}

* {
box-sizing: border-box;
margin: 0;
padding: 0;
}

nav {
    background-color: #2a6495;
    border-right: 2px solid #c0392b;
    border-top-right-radius: 40px 40px;
    border-bottom-right-radius: 40px 40px;
    color: #FFF;
    position: fixed;
    top: 0;
    left: 0;
    width: 60px;
    height: 40%;
    z-index: 100;
    transform: translateX(-80%);
    transition: transform 250ms ease-out;
}

nav:hover {
    transform: translateX(0px);
}

nav ul {
    padding:0;
    list-style: none;
    margin: 0;
}

nav ul li {
    border-bottom: 2px solid rgba(200, 200, 200, 0.1);
    padding: 20px;
}

nav ul li:first-of-type {
    border-top: 2px solid rgba(200, 200, 200, 0.1);
}

nav ul li a {
    color: #fff;
    text-decoration: none;
}

nav ul li a:hover {
    color: yellowgreen;
}

header {
    position: relative;
    text-align: center;
    margin: 15px 0;
}

header h1 {
    margin: 40px 0 15px 0;
}

header p {
    margin: 0;
    color: red;
}

.container {
    position: relative;
    text-align: center;
    height: 100%;
    width: 100%;
    background: #BBB;
}

.infomation {
    height: 100%;
}

.function-area {
    text-align: right;
    height: 50px;
}

.function-area span {
    display: block;
    margin-top: 10px;
}

.function-area span a {
    text-decoration: none;
    font-size: 14px;
    color: black;
}


.footer {
    background: #55b7a4;
    color: #212121;
    position: fixed;
    z-index: 100;
    bottom: 0;
    left: 0;
    width: 100%;
}
```

