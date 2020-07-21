# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>
  
# 双飞翼
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

# 四类定位
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

# 经典层叠
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

# 解决inline-box间隙问题
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

# 基于视口垂直居中
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
# 定宽垂直居中
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

# transform垂直居中
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

# flex垂直居中方法1
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


# flex垂直居中方法2
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

# text-align的center属性水平居中
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

# margin的auto属性 水平居中
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

# 绝对定位水平居中
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

# 相对定位水平居中
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

# 使用div绘制图形（三角形）——进阶可以学习clip-path的用法画各种图形！
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



***

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

