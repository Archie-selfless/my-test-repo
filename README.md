# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>
    Here is my skill list:
  * 111
  * 222
# html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- 使用viewport进行移动端页面布局的控制。以下内容说明：[宽度适应设备] + [初始缩放比例1:1]-->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!--  优先使用最新的IE版本  -->
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <link rel="stylesheet" href="validate.css">
    <title>登录界面</title>
</head>
<body>
    <div class="container">
        <form id="form" class="form">
            <h2>注册</h2>
            <div class="form-control">
                <label for="username">姓名:</label>
                <input type="text" id="username" placeholder="请输入姓名">
                <small>Error message</small>
            </div>
            <div class="form-control">
                <label for="email">邮箱:</label>
                <input type="text" id="email" placeholder="请输入邮箱">
                <small>Error message</small>
            </div>
            <div class="form-control">
                <label for="pwd">输入密码:</label>
                <input type="password" id="pwd" placeholder="请输入密码">
                <small>Error message</small>
            </div>
            <div class="form-control">
                <label for="pwd2">确认密码:</label>
                <input type="password" id="pwd2" placeholder="再次输入密码">
                <small>Error message</small>
            </div>
            <button type="submit">提交</button>
        </form>
    </div>
    <script src="validate.js"></script>

</body>
</html>
```

# css
``` (css)
/* CSS提供的导入，此处将谷歌的字体资源库导入 */
@import url('https://fonts.googleapis.com/css?family=Open+Sans&display=swap');

/* CSS声明全局量，需使用时可通过var()函数调用 */
:root {
    --success-color: #2ecc71;
    --error-color: #e74c3c;
    --background-color: #d1eeff
}

/*border-box 告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。*/
/*也就是说，如果你将一个元素的width设为100px,*/
/*那么这100px会包含其它的border和padding，内容区的实际宽度会是width减去border + padding的计算值。*/
/*大多数情况下这使得我们更容易的去设定一个元素的宽高*/
* {
    box-sizing: border-box;
}

/* 这是 当文档处于 Quirks模式 时IE使用的盒模型*/

body {
    background-color: var(--background-color);
    font-family: 'Open Sans', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
}

.container {
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

h2 {
    text-align: center;
}

.form {
    padding: 30px 40px;
}

.form-control {
    position: relative;
    margin-bottom: 20px;
    padding-bottom: 10px;
}

.form-control label {
    color: #777;
    display: block;
}

.form-control input {
    border: 2px solid #f0f0f0;
    border-radius: 4px;
    display: block;
    width: 100%;
    font-size: 14px;
}

.form-control input:focus{
    outline: 0;
    border-color: #777;
}

.form-control small {
    color: var(--error-color);
    position: absolute;
    bottom: 0;
    left: 0;
    visibility: hidden;
}

.form-control.success input {
    border-color: var(--success-color);
}

.form-control.error input {
    border-color: var(--error-color);
}

.form-control.error small {
    visibility: visible;
}

.form button {
    cursor: pointer;
    background-color: #3498db;
    border: 2px solid #3498db;
    border-radius: 4px;
    color: #fff;
    display: block;
    font-size: 16px;
    padding: 10px;
    margin-top: 20px;
    width: 100%;
}
```

# js
```
const form = document.getElementById('form');
const username = document.getElementById('username');
const email = document.getElementById('email');
const pwd = document.getElementById('pwd');
const pwd2 = document.getElementById('pwd2');

// 展示错误信息 Error message
function showError(input, message) {
    const formControl = input.parentElement;
    formControl.className = 'form-control error';
    const small = formControl.querySelector('small');
    small.innerText = message;
}
// 展示成功大纲
function showSuccess(input) {
    const formControl = input.parentElement;
    formControl.className = 'form-control success';
}

form.addEventListener('submit', function (e) {
    e.preventDefault(); // 禁止掉浏览器的默认事件,只让浏览器执行我们规定的函数.


}, { passive: false, capture: false });
/*
* capture: 表示函数是否捕获执行,
* passive: 表示是否执行默认事件，true执行，false不执行
* once: 是否是单次事件，如果是true，执行完事件就被销毁
* */
```
