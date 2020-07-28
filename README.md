# my-test-repo
# 日常记录用测试型仓库
  [My CSDN](http://blog.csdn.net/archiewade "点击跳转")<br>
  [My Blog](https://archieself.online)<br>
  [掘金]()<br>
***

## 十进制转换为任意N进制
```javascript
/* 通过数组实现 数据结构——栈 */
function Stack() {
    let items = [];

    /* 压栈 */
    this.push = function (element) {
        return items.push(element);
    };

    /* 弹出栈 */
    this.pop = function () {
        return items.pop();
    };

    /* 判定栈空 */
    this.idEmpty = function () {
        return items.length == 0;
    }
}

function Decimal2Binary(number) {
    let myStack = new Stack(), // 存放筛选值的栈
        reminder,  // 每次求余后的余数
        binaryString = '';  // 二进制字符串

    while (number > 0) {
        reminder = Math.floor(number % 2); // 十进制数对2除余
        myStack.push(reminder);
        number = Math.floor(number/2); // 获得除余后的 商
    }

    while (! myStack.idEmpty()) {
        binaryString += myStack.pop().toString();
    }

    console.log(binaryString);
}

Decimal2Binary(155); //10011011
```

## 数组去重
ES6 新增了 Set 这一数据结构，类似于数组，但 Set 的成员具有唯一性
基于这一特性，就非常适合用来做数组去重
```javascript
var arr1 = Array.from(new Array(10), (x, index) => {return index * 2});
var arr2 = Array.from(new Array(20), (x, index) => {return index});

console.log(arr1); // [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
console.log(arr2); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]

function distinct(a, b) {
    let c = a.concat(b); // 整合两个数组（简单拼接）
    return [...new Set(c)]; // 简单明了
}

var result = distinct(arr1, arr2);
console.log(result);  // [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

## 快速生成0~100数组
```javascript
Array.from({length:30},(x, index) => {return index + 1});
```

## 随机生成任意区间数的公式
```javascipt
//如果你希望生成任意值到任意值的随机数，公式就是这样的：
// max - 期望的最大值
// min - 期望的最小值 
parseInt(Math.random()*(max-min+1)+min,10);
Math.floor(Math.random()*(max-min+1)+min);

var max =10;
var min = 1;
var arrays = Array.from({length:20},
    ()=>Math.floor(Math.random()*(max-min+1)+min)); // 生成长度20，每个元素1~10的随机数组
```

## 快速进制转换
```javascript
//十进制转其他进制
var x=110;
console.log(x);
console.log(x.toString(8));
console.log(x.toString(32));
console.log(x.toString(16));

//字符串解析为指定进制后 转十进制
var x='110';
console.log(parseInt(x,2));
console.log(parseInt(x,8));
console.log(parseInt(x,16));
```

## 使用Set完成 交并补
```javascript
const arr1 = [1,2,4,5,9];
const arr2 = [3,7,5,9];
const unionSet = new Set([...arr1, ...arr2]);
const filterSet = new Set([9]);
const interSet = new Set(
    [...unionSet].filter(item => filterSet.has(item))
);
const pureSet = new Set(
    [...unionSet].filter(item => !filterSet.has(item))
);

console.log(unionSet); // Set并集
console.log(interSet); // Set交集
console.log(pureSet); // Set差集
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


