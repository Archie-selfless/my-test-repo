# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>
# DOM Array Methods
## html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="x-ua-compatible" content="id=edge">
    <link rel="stylesheet" href="dommethod.css">
    <title>DOM Methods</title>
</head>
<body>

<h1>Dom Array Methods</h1>
<div class="container">
    <aside>
        <button id="add-user">添加用户</button>
        <button id="double">金钱翻倍</button>
        <button id="show-millionaires">只展示百万富翁</button>
        <button id="sort">按财富排序</button>
        <button id="calculate-wealth">计算全体财富值</button>
    </aside>

    <!--    通常main标签可以当做界标使用    -->
    <main id="main">
        <h2><strong>Person</strong>Wealth</h2>
    </main>
</div>

<!--<script src="dommethod.js"></script>-->
<script>
    let number = 3.09887;
    console.log(number.toFixed(2));
</script>
</body>
</html>
```

## css
``` (css)
* {
    box-sizing: border-box;
}

body {
    background: #f4f4f4;
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
}

.container {
    display: flex;
    padding: 20px;
    margin: 0 auto;
    max-width: 100%;
    width: 800px;
}

aside {
    padding: 10px 20px;
    width: 250px;
    border-right: 1px solid #111;
}

button {
    cursor: pointer;
    background-color: #ffffff;
    border: solid 1px #111;
    border-radius: 5px;
    display: block;
    width: 100%;
    margin: 10px 0;
}

#main {
    flex: 1;
    padding: 10px 20px;
}

h2 {
    border-bottom: 1px solid #111;
    padding: 0 10px;
    display: flex;
    justify-content: space-between;
    margin:  0 0 20px;
}
```

## js
```
const main = document.getElementById('main');
const addUserBtn = document.getElementById('add-user');
const doubleBtn = document.getElementById('double');
const showMillionairesBtn = document.getElementById('show-millionaires');
const sortBtn = document.getElementById('sort');
const calculateWeathBtn = document.getElementById('calculate-wealth');

let data = [];

getRandomUser();
getRandomUser();

// 获取随机用户并添加金额
async function getRandomUser() {
    /* randomuser.me 会返回一个JSON化的对象，包含多种常用User数据 */
    const res = await fetch('https://randomuser.me/api');
    const data = await res.json();
    const user = data.results[0];
    const newUser = {
        name: user.name.first + ' ' + user.name.last,
        money: Math.floor(Math.random() * 10000000)
    };
    addData(newUser);
}

// 在数据组中添加新对象
function addData(obj) {
    data.push(obj);
    updateDOM();
}

// 所有人金额翻倍
function doubleMoney() {
    data = data.map(user => {
        return {...user, money: user.money * 2};
    });
    updateDOM();
}

// 按富有级别降序
function sortByRichest() {
    data.sort((a, b) => b.money - a.money);
    updateDOM();
}

// 展示百万富翁
function showMillionaires() {
    data = data.filter(user => user.money > 1000000);
    updateDOM();
}

// 计算财富总值
function calculateWealth() {
    const wealth = data.reduce((acc, user) => (acc += user.money), 0);
    const wealthEL = document.createElement('div');
    wealthEL.innerHTML = '<h3>Total: <strong>' + formatMoney(wealth) + '</strong>></h3>>';
    main.appendChild(wealthEL);
}

// 更新DOM
function updateDOM(providedData = data) {
    // 清除main div
    main.innerHTML = "<h2><strong>Person</strong>Wealth</h2>";

    providedData.forEach(item => {
        const element = document.createElement('div');
        element.classList.add('person');
        element.innerHTML = '<strong>' + item.name + '</strong>' + formatMoney();
        main.appendChild(element);
    });
}

// 将数组转化为金额
function formatMoney(number) {
    return '$' + number.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
}
```

