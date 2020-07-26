# my-test-repo
# 日常记录用测试型仓库
  [My CSDN](http://blog.csdn.net/archiewade "点击跳转")<br>
  [My Blog](https://archieself.online)<br>
  [掘金]()<br>

***

# JS基础-Hoisting
通常JS引擎会在正式执行之前先进行一次预编译（不同JS引擎的编译形式不同），在这个过程中，首先将`变量声明`及`函数声明` **提升至当前作用域的顶端**，然后进行接下来的处理
**JavaScript没有块作用域，只有全局作用域和函数作用域** <br>
## 变量提升(起初人为实现的遗留纰漏)
e.g.
```javascript
if (!foo) {
    var foo = 5;
}
```
转换为如下
```javascript
var foo;
if (!foo) {
    foo = 5;
}
```
## 函数提升(为解决相互递归而提出的策略)
e.g.
```javascript
function hoistFunction() {
    function foo() { // 首先被提升
        console.log(1);
    }

    foo(); // output: 2

    function foo() { // 之后被提升，且覆盖之前的同名函数
        console.log(2);
    }
}
```
#### 当函数声明遇到函数表达式
```
function hoistFunction() {
    foo(); // 2

    var foo = function() {
        console.log(1);
    };

    foo(); // 1

    function foo() {
        console.log(2);
    }

    foo(); // 1
}
```
**JavaScript中的函数是一等公民**，`函数声明的优先级最高`，会被提升至当前作用域最顶端，所以第一次调用时实际执行了下面定义的函数声明，然后第二次调用时，由于前面的函数表达式与之前的函数声明同名，故将其覆盖，以后的调用也将会打印同样的结果<br>

*虽然在ES6中，用let代替var更可靠，但是ES6中的class声明也存在提升，而且`class\le\const`都被约束和限制了，如果在声明位置之前引用，则是不合法的，会抛出一个异常*

> 所以，为了更可靠、可维护性更高，无论是早期的代码，还是ES6中的代码，变量还是函数，都必须先声明后使用！

# JS·ES6——箭头函数
> 语法<br>
(参数1, 参数2, …, 参数N) => { 函数声明 } <br>
(参数1, 参数2, …, 参数N) => 表达式(单一)/{ return 表达式; } 

当只有一个参数时，圆括号是可选的
> (单一参数) => {函数声明} <br>
单一参数 => {函数声明}

没有参数的函数应该写成一对圆括号
> () => {函数声明}

**注意点**
* 有的箭头函数都没有自己的 this。 不适合定义一个 对象的方法
* 当我们使用箭头函数的时候，箭头函数会**默认帮我们绑定外层 this 的值**，所以在箭头函数中 this 的值和外层的 this 是一样的。
* **箭头函数是不能提升的**，所以需要在使用之前定义。
* 使用 `const` 比使用 `var` 更安全，因为**函数表达式始终是一个常量**。
* 如果函数部分只是一个语句，则可以省略 `return` 关键字和大括号 `{}`，这样做是一个比较好的习惯:

# JS基础——this
> 面向对象语言中 this 表示当前对象的一个引用。 <br>
但在 JavaScript 中 this 不是固定不变的，它会**随着执行环境的改变而改变**
* 在方法中，this 表示该方法所属的对象。
* 如果单独使用，this 表示全局(Global)对象。
* 在函数中，this 表示全局(Global)对象。
* 在函数中，在`严格模式`下，this 是未定义的(undefined)。
* 在事件中，this 表示接收事件的元素。
* 类似 call() 和 apply() 方法可以将 this 引用到任何对象
  * 异常强大的功能！具体如下:
  ```javascript
  var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
  }
   var person2 = {
   firstName:"John",
   lastName: "Doe",
  }
  /* 当我们使用 person2 作为参数来调用 person1.fullName 方法时, 
  this 将指向 person2, 即便它是 person1 的方法 */
  person1.fullName.call(person2);  // 返回 "John Doe"
  ```

# JS基础——addEventListener()
> addEventListener() 方法用于向指定元素添加事件句柄,且不会覆盖已存在的事件句柄 <br>
可以向同个元素添加多个同类型的事件句柄，如：两个 "click" 事件。 <br>
可以向任何 DOM 对象添加事件监听，不仅仅是 HTML 元素。如： window 对象 <br>
语法：`element.addEventListener(event, function, useCapture);`

#### 事件冒泡或事件捕获
<p> 元素插入到 <div> 元素中,根据`useCapture`的不同产生不同情况：<br>
  在 *冒泡*(false) 中，内部元素的事件会先被触发，然后再触发外部元素，即： <p> 元素的点击事件先触发*。
  在 *捕获*(true) 中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div> 元素的点击事件先触发 *。

#### 移除事件句柄
> 语法：`element.removeEventListener("event", function);`

**注意点**
IE 8 及更早 IE 版本，Opera 7.0及其更早版本不支持 addEventListener() 和 removeEventListener() 方法<br>
可以使用 attachEvent(event, function)/detachEvent(event, function)实现相同功能<br>
所以为了兼容所有的浏览器，我们可以定义一个函数：当有 addEventListener 时调用，没有的时候调用 attachEvent
```javascript
function bind(obj , eventStr , callback){
    if(obj.addEventListener){
        //大部分浏览器
        obj.addEventListener(eventStr , callback , false);
    }else{
        //IE8及以下
        obj.attachEvent("on"+eventStr , function(){
            //在匿名函数中调用回调函数
            callback.call(obj);
        });
    }
}  
```

# JS基础——闭包
> 为了实现`私有变量`，我们用到一个JS重要机制：<br>
**所有函数都能访问它们上一层的作用域**<br>
于是，在函数内嵌套函数，从而达到`私有化`

```javascript
function add() {
    /* 每次调用add()都会将当前作用域的counter初始化为0，然后再+1 */
    var counter = 0;
    return counter += 1;
}
 
add();
add();
add();
 
// 本意是想输出 3, 但事与愿违，输出的都是 1 !
```

```javascript
/* 立即函数只执行一次后留下'( )'的外壳，保护counter不被销毁，这就是闭包！
直观的说就是形成一个不销毁的栈环境 */
var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();
 
add();
add();
add();
 
// 计数器为 3
```

# JS基础——querySelector..和getElementBy..
#### 区别1
* getElementByTagName 方法返回的结果是 `HTMLCollection`
* getElementById 方法返回的结果是 `NodeList`
* query 方法返回的结果是 `NodeList`
#### 区别2
* query 选择符选出来的元素是`静态`（元素不会随着文档操作而改变）的
* getElement 这种方法选出的元素的动态的

HTML:
```html
<ul>
    <li>111</li>
    <li>222</li>
    <li>333</li>
</ul>
```
JS:
```javascript
var ul=document.querySelector('ul');
var list=ul.querySelectorAll('li');
for(var i=0;i<3;i++){
    ul.appendChild(document.createElement('li'));
}
//    这时创建了3个新li，添加在ul列表中
console.log(list.length)
//    输出3，输出的是添加前li的数量，而非此时li的总数量6
```
**重点(有意思)**
```javascript
function getElementA() {
        var test = document.getElementById('test');
        var list = document.getElementsByTagName('li');

        console.log(list.length);

        for (var i = 0; i < list.length; i ++) {
            test.appendChild(document.createElement('li'));
        }

        console.log(list);
    }

    function queryB() {
        let ul = document.querySelector('ul');
        let list = ul.querySelectorAll('li');
        for (var i = 0; i < 3; i++) {
            ul.appendChild(document.createElement('li'));
        }
        console.log(list);
    }

    getElementA();
```




















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

