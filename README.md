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

# Test
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
        .layout.flex .left-main{
            display: flex;
        }
        .layout.flex .left{
            background-color: #4d4d4d;
            width: 300px;
        }
        .layout.flex .main{
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

</body>
</html>
```
## CSS
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
