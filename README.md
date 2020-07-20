# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>
  
# 双栏布局
## test.css
```
* {
    margin: 0;
    padding: 0;
}
.layout {
    margin-top: 10px;
}
.layout div {
    min-height: 100px;
}
```
## test.html
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
<!--1.浮动的方式来实现布局-->
<section class="layout float">
    <style>
        .layout.float .left {
            float: left;
            width: 100px;
            background-color: #4d4d4d;
        }

        .layout.float .main {
            background-color: #2a6495;
        }
    </style>
    <article class="left-main">
        <div class="left"></div>
        <div class="main">
            <h1>浮动双栏布局</h1>
            <p>双栏布局中间部分</p>
            <p>双栏布局中间部分</p>
        </div>
    </article>
</section>

<!--2.定位的方式来实现布局-->
<section class="layout absolute">
    <style>
        .layout.absolute .left-main {
            width: 100%;
        }

        .layout.absolute .left {
            position: absolute;
            left: 0;
            width: 200px;
            background-color: #4d4d4d;
        }

        .layout.absolute .main {
            margin-left: 200px;
            background-color: #2a6495;
            right: 0;
        }
    </style>
    <article class="left-main">
        <div class="left"></div>
        <div class="main">
            <h1>绝对定位双栏布局</h1>
            <p>双栏布局中间部分</p>
            <p>双栏布局中间部分</p>
        </div>
    </article>
</section>

<!--3.flex布局的实现-->
<section class="layout flex">
    <style>
        .layout.flex .left-main {
            display: flex;
        }

        .layout.flex .left {
            background-color: #4d4d4d;
            width: 300px;
        }

        .layout.flex .main {
            background-color: #2a6495;
            flex: 1;
        }
    </style>
    <article class="left-main">
        <div class="left"></div>
        <div class="main">
            <h1>flex双栏布局</h1>
            <p>双栏布局中间部分</p>
            <p>双栏布局中间部分</p>
        </div>
    </article>
</section>

<!-- 4.table布局的实现 -->
<section class="layout table">
    <style>
        .layout.table .left-main {
            display: table;
            width: 100%;
        }

        .layout .left {
            display: table-cell;
            width: 400px;
            background-color: #4d4d4d;
        }

        .layout .main {
            background-color: #2a6495;
        }
    </style>
    <article class="left-main">
        <div class="left"></div>
        <div class="main">
            <h1>table双栏布局</h1>
            <p>中间布局部分</p>
            <p>中间布局部分</p>
        </div>
    </article>
</section>

<!-- 5.grid布局 -->
<section class="layout grid">
    <style>
        .layout.grid .left-main {
            display: grid;
            grid-template-rows: 100px;
            grid-template-columns: 100px auto;
        }
        .layout.grid .left {
            background-color: #4d4d4d;
        }
        .layout.grid .main {
            background-color: #2a6495;
        }
    </style>
    <article class="left-main">
        <div class="left"></div>
        <div class="main">
            <h1>grid双栏布局</h1>
            <p>双栏布局中间部分</p>
            <p>双栏布局中间部分</p>
        </div>
    </article>
</section>
</body>
</html>
```
# 圣杯布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo</title>
    <style>
        .right, .left, .main {
            min-height: 100px;
            float: left;
            position: relative;
        }
        .left{
            width: 200px;
            background-color: #2a6495;
            margin-left: -100%; /* 使左侧区块移至中心块之前 */
            left: -200px; /* 顶去容器的左内间距 */
        }
        .right {
            width: 300px;
            background-color: #2a5b52;
            margin-left: -300px; /* 使右侧区块移至中心块之后 */
            right: -300px; /* 顶去容器的右内间距 */
        }
        .main {
            background-color: #000;
            width: 100%;
        }
        .container {
            padding-left: 200px;
            padding-right: 300px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="main"></div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
</body>
</html>
```
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
# 定宽居中
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

