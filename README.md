# my-test-repo
# 日常记录用测试型仓库
  [My blog](http://blog.csdn.net/archiewade "点击跳转")<br><br>

# 排行确认
##HTML
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="x-ua-compatible" content="ie=egde">
    <title>十大富豪</title>
    <link rel="stylesheet" href="list.css">
    <script src="https://kit.fontawesome.com/3da1a747b2.js" crossorigin="anonymous"></script>
</head>
<body>
<h1>10 Richest People</h1>
<p>将人员拖放到相应的位置</p>
<ul class="draggable-list" id="draggable-list"></ul>
<button class="check-btn" id="check">
    Check Order
    <i class="fas fa-paper-plane"></i>
</button>

<script src="list.js"></script>
</body>
</html>
```
#CSS
```
@import url('http://fonts.googleapis.com/css?family=Lato&display=swap');

:root {
    --border-color: #e2e5e4;
    --background-color: #c3c7ca;
    --text-color: #35444f
}

* {
    box-sizing: border-box;
}

body {
    background-color: #f0f0f0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    height: 100vh;
    margin: 0;
    font-family: 'Lato', sans-serif;
}

.draggable-list {
    border: 1px solid var(--border-color);
    color: var(--text-color);
    padding: 0;
    list-style-type: none;
}

.draggable-list li {
    background-color: #fff;
    display: flex;
    flex: 1;
}

.draggable-list li:not(:last-of-type) {
    border-bottom: 1px solid var(--border-color);
}

.draggable-list .number {
    background-color: var(--background-color);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 28px;
    height: 60px;
    width: 60px;
}

.draggable-list li.over .draggable {
    background-color: #eaeaea;
}

.draggable-list .person-name {
    margin: 0 20px 0 0;
}

.draggable-list li.right .person-name {
    color: #3ae374;
}

.draggable-list li.wrong .person-name {
    color: #ff3838;
}

.draggable {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 15px;
    flex: 1;
}

.check-btn {
    background-color: var(--background-color);
    border: none;
    color: var(--text-color);
    font-size: 16px;
    padding: 10px 20px;
    cursor: pointer;
}

.check-btn:active {
    transform: scale(0.98);
}

.check-btn:focus {
    outline: none;
}
```
#JS
```
const draggable_list = document.getElementById('draggable-list');
const check = document.getElementById('check');

const richestPeople = [
    'Jeff Bezos',
    'Bill Gates',
    'Warren Buffett',
    'Bernard Arnault',
    'Carlos Slim Helu',
    'Amancio Ortega',
    'Larry Ellison',
    'Mark Zuckerberg',
    'Michael Bloomberg',
    'Larry Page'
];

// 存储人员项
const listItems = [];

let dragStartIndex;

createList();

// Insert list items into DOM
function createList() {
    [...richestPeople]
        .map(a => ({ value: a, sort: Math.random() }))
        .sort((a, b) => a.sort - b.sort)
        .map(a => a.value)
        .forEach((person, index) => {
            const listItem = document.createElement('li');

            listItem.setAttribute('data-index', index);

            listItem.innerHTML = `
        <span class="number">${index + 1}</span>
        <div class="draggable" draggable="true">
          <p class="person-name">${person}</p>
          <i class="fas fa-grip-lines"></i>
        </div>
      `;

            listItems.push(listItem);

            draggable_list.appendChild(listItem);
        });

    addEventListeners();
}

function dragStart() {
    // console.log('Event: ', 'dragstart');
    dragStartIndex = +this.closest('li').getAttribute('data-index');
}

function dragEnter() {
    // console.log('Event: ', 'dragenter');
    this.classList.add('over');
}

function dragLeave() {
    // console.log('Event: ', 'dragleave');
    this.classList.remove('over');
}

function dragOver(e) {
    // console.log('Event: ', 'dragover');
    e.preventDefault();
}

function dragDrop() {
    // console.log('Event: ', 'drop');
    const dragEndIndex = +this.getAttribute('data-index');
    swapItems(dragStartIndex, dragEndIndex);

    this.classList.remove('over');
}

// Swap list items that are drag and drop
function swapItems(fromIndex, toIndex) {
    const itemOne = listItems[fromIndex].querySelector('.draggable');
    const itemTwo = listItems[toIndex].querySelector('.draggable');

    listItems[fromIndex].appendChild(itemTwo);
    listItems[toIndex].appendChild(itemOne);
}

// Check the order of list items
function checkOrder() {
    listItems.forEach((listItem, index) => {
        const personName = listItem.querySelector('.draggable').innerText.trim();

        if (personName !== richestPeople[index]) {
            listItem.classList.add('wrong');
        } else {
            listItem.classList.remove('wrong');
            listItem.classList.add('right');
        }
    });
}

function addEventListeners() {
    const draggables = document.querySelectorAll('.draggable');
    const dragListItems = document.querySelectorAll('.draggable-list li');

    draggables.forEach(draggable => {
        draggable.addEventListener('dragstart', dragStart);
    });

    dragListItems.forEach(item => {
        item.addEventListener('dragover', dragOver);
        item.addEventListener('drop', dragDrop);
        item.addEventListener('dragenter', dragEnter);
        item.addEventListener('dragleave', dragLeave);
    });
}

check.addEventListener('click', checkOrder);

```
# 歌词搜索
## HTML
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <link rel="stylesheet" href="lyrics.css">
    <title>歌词搜索</title>
</head>
<body>
    <header>
        <h1>歌词搜索</h1>
        <input type="text" id="search" placeholder="请输入短文或歌名">
        <button>Search</button>
    </header>

    <div id="result" class="container">
        <p>结果展示如下</p>
    </div>

    <div id="more" class="container centered"></div>
</body>
</html>
```
## CSS
```
* {
    box-sizing: border-box;
}

body {
    background-color: #fff;
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
}

button {
    cursor: pointer;
}

button:active {
    transform: scale(0.95); /* 缩放函数，param1-水平缩放值，param2-垂直缩放值 */
}

/*对于很多元素来说，如果没有设置样式，轮廓是不可见的。
因为样式（style）的默认值是 none。
但 input 元素是例外，其样式默认值由浏览器决定。*/
input:focus,
button:focus {
    outline: none; /* 文本框和按钮获得焦点时，去除轮廓 */
}

header {
    /* background-image 属性用于为一个元素设置一个或者多个背景图像 ，第一个图像“最接近用户” */
    background-image: url('https://images.unsplash.com/photo-1510915361894-db8b60106cb1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80');
    /* 图像不会被重复. 那个没有被重复的背景图像的位置是由background-position属性来决定. */
    background-repeat: no-repeat;
    /* 将原图像缩放，直到能完全覆盖背景区域 */
    background-size: cover;
    background-position: center center;
    color: #fff;
    display: flex;
    /* flex容器的主轴和块轴相同。主轴起点与主轴终点和书写模式的前后点相同 */
    flex-direction: column;
    /* 元素在侧轴居中。如果元素在侧轴上的高度高于其容器，那么在两个方向上溢出距离相同。 */
    align-items: center;
    /* 伸缩元素向每行中点排列。每行第一个元素到行首的距离将与每行最后一个元素到行尾的距离相同。 */
    justify-content: center;
    padding: 100px 0;
    position: relative;
}

header::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.4);
}

header * {
    z-index: 1;
}

header h1 {
    margin: 0 0 30px;
}

form {
    position: relative;
    width: 500px;
    max-width: 100%;
}

form input {
    border: 0;
    border-radius: 50px;
    font-size: 16px;
    padding: 15px 30px;
    width: 100%;
}

form button {
    position: absolute;
    top: 2px;
    right: 2px;
    background-color: #e056fd;
    border: 0;
    border-radius: 50px;
    color: #fff;
    font-size: 16px;
    padding: 13px 30px;
}

.btn {
    background-color: #8d56fd;
    border: 0;
    border-radius: 10px;
    color: #fff;
    padding: 4px 10px;
}

ul.songs {
    list-style-type: none;
    padding: 0;
}

ul.songs li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 10px 0;
}

.container {
    margin: 30px auto;
    max-width: 100%;
    width: 500px;
}

.container h2 {
    font-weight: 300;
}

.container p {
    text-align: center;
}

.centered {
    display: flex;
    justify-content: center;
}

.centered button {
    transform: scale(1.3);
    margin: 15px;
}

```
## JS
```
const form = document.getElementById('form');
const search = document.getElementById('search');
const result = document.getElementById('result');
const more = document.getElementById('more');

const apiURL = 'https://api.lyrics.ovh';

// Search by song or artist
async function searchSongs(term) {
    const res = await fetch(`${apiURL}/suggest/${term}`);
    const data = await res.json();

    showData(data);
}

// Show song and artist in DOM
function showData(data) {
    result.innerHTML = `
    <ul class="songs">
      ${data.data
        .map(
            song => `<li>
      <span><strong>${song.artist.name}</strong> - ${song.title}</span>
      <button class="btn" data-artist="${song.artist.name}" data-songtitle="${song.title}">Get Lyrics</button>
    </li>`
        )
        .join('')}
    </ul>
  `;

    if (data.prev || data.next) {
        more.innerHTML = `
      ${
            data.prev
                ? `<button class="btn" onclick="getMoreSongs('${data.prev}')">Prev</button>`
                : ''
        }
      ${
            data.next
                ? `<button class="btn" onclick="getMoreSongs('${data.next}')">Next</button>`
                : ''
        }
    `;
    } else {
        more.innerHTML = '';
    }
}

// Get prev and next songs
async function getMoreSongs(url) {
    const res = await fetch(`https://cors-anywhere.herokuapp.com/${url}`);
    const data = await res.json();

    showData(data);
}

// Get lyrics for song
async function getLyrics(artist, songTitle) {
    const res = await fetch(`${apiURL}/v1/${artist}/${songTitle}`);
    const data = await res.json();

    if (data.error) {
        result.innerHTML = data.error;
    } else {
        const lyrics = data.lyrics.replace(/(\r\n|\r|\n)/g, '<br>');

        result.innerHTML = `
            <h2><strong>${artist}</strong> - ${songTitle}</h2>
            <span>${lyrics}</span>
        `;
    }

    more.innerHTML = '';
}

// Event listeners
form.addEventListener('submit', e => {
    e.preventDefault();

    const searchTerm = search.value.trim();

    if (!searchTerm) {
        alert('Please type in a search term');
    } else {
        searchSongs(searchTerm);
    }
});

// Get lyrics button click
result.addEventListener('click', e => {
    const clickedEl = e.target;

    if (clickedEl.tagName === 'BUTTON') {
        const artist = clickedEl.getAttribute('data-artist');
        const songTitle = clickedEl.getAttribute('data-songtitle');

        getLyrics(artist, songTitle);
    }
});

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
