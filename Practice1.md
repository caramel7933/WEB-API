## `1`- 用户名 显示隐藏内容

- 题目描述

- 显示和隐藏输入框中的提示内容

    1）输入框获得焦点，提示内容消失，边框变色

    2）输入框失去焦点，如果内容为空，提示内容恢复，边框变色；如果内容不为空，只有边框变色
```html
    <style>
        input {
            color: #999;
            border: 1px solid #ccc;
            outline: none;
        }
    </style>
<body>
    <input type="text" value="邮箱/ID/手机号">
    <script>
        var input = document.querySelector('input');
        // 获得焦点
        input.onfocus = function() {
            if (this.value === '邮箱/ID/手机号') {
                this.value = '';
                this.style.border = '1px solid pink';
            } 
        }
        // 失去焦点
        input.onblur = function() {
            if (this.value === '') {
                this.value = '邮箱/ID/手机号';
                this.style.border = '1px solid #ccc';
            }
        }
    </script>
</body>
```

## `2`- 关闭广告（直接隐藏即可）

- 训练目标

    能够操作元素的样式属性

- 训练提示

    1.获取要操作的关闭按钮和广告元素

    2.关闭按钮注册单击事件

    3.隐藏广告元素

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        .box {
            position: relative;
            height: 80px;
        }
        .box img {
            width: 100%;
        }
        .close-btn {
            position: absolute;
            top: 2px;
            right: 2px;
            width: 20px;
            height: 20px;
            font-size: 12px;
            font-family: Arial, Helvetica, sans-serif;
            line-height: 20px;
            text-align: center;
            background-color: rgba(0, 0, 0, .2);
            color: red;
            cursor: pointer;
        }
    </style>
<body>
    <div class="box">
        <img src="luzhou.jpg" alt="">
        <i class="close-btn">X</i>
    </div>
    <script>
        var box = document.querySelector('.box');
        var btn = document.querySelector('.close-btn');
        btn.onclick = function() {
            box.style.display = 'none';
        }
    </script>
</body>
```

## `3`- 下拉菜单

- 题目描述

    鼠标移入显示下拉菜单，鼠标移出隐藏下拉菜单

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        li {
            list-style: none;
        }
        a {
            text-decoration: none;
            font-size: 14px;
        }
        .nav {
            margin: 100px;
        }
        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }
        .nav>li>a:hover {
            background-color: #eee;
        }
        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }
        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border: 1px solid #FECC5B;
            border-top: none;
        }
        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
</head>
<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="#">评论</a>
                </li>
                <li>
                    <a href="#">私信</a>
                </li>
                <li>
                    <a href="#">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="#">评论</a>
                </li>
                <li>
                    <a href="#">私信</a>
                </li>
                <li>
                    <a href="#">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="#">评论</a>
                </li>
                <li>
                    <a href="#">私信</a>
                </li>
                <li>
                    <a href="#">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="#">评论</a>
                </li>
                <li>
                    <a href="#">私信</a>
                </li>
                <li>
                    <a href="#">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        var nav = document.querySelector('.nav');
        var lis = nav.children;
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function() {
                this.children[1].style.display = 'block';
            }
            lis[i].onmouseout = function() {
                this.children[1].style.display = 'none';
            }
        }
    </script>
</body>
```

## `4`- 网页开关灯

- 题目描述

    单击按钮，控制网页开关灯

- 训练提示

    1.获取要操作的按钮和body元素

    2.给按钮注册单击事件

    3.使用全局变量记录灯的状态

    4.根据灯的状态，控制body元素的背景色，实现开关灯效果

```html
<body>
    <button id="btn">开关灯</button>
    <script>
        var btn = document.querySelector('#btn');
        var flag = 0;
        btn.onclick = function() {
            if (flag == 0) {
                document.body.style.backgroundColor = 'black';
                flag = 1;
            }   else {
                document.body.style.backgroundColor = '#fff';
                flag = 0;
            }
        }
    </script>
</body>
```

## `5`- 获取元素

- 单选题

    关于获取元素,以下描述正确的是:

```
    A，document.getElementById()获取到的是元素集合

    B，document.getElementsByTagName()获取到的是单个元素

    C， document.querySelector()获取到的是元素集合

    D， document.getElementsByClassName()有浏览器兼容性问题
```
答案: D

解析: A选项，返回的是单个元素对象或null；B选项返回的是元素集合；C选项返回的单个元素对象；D选项，是h5新增的方法，所以有浏览器兼容性问题

- 单选题

    关于获取元素,以下获取到单个元素的方法是:

```
    A，document.getElementById()

    B，document.getElementsByTagName()

    C， document.querySelectorAll()

    D， document.getElementsByClassName()
```
答案: D

解析: A选项，返回的是单个元素对象或null

- 多选题

    关于获取元素,以下获取到元素集合的方法是:

```
    A，document.getElementById()

    B，document.getElementsByClassName()

    C， document.querySelector()

    D， document.querySelectorAll()
```

答案: BD

解析: B选项和D选项，返回的是元素集合；

## `6`- 注册事件

- 多选题

    关于事件，下列描述正确的是：

```
    A，当页面一打开，所有的事件就会被触发

    B，注册事件的格式为： 事件源.事件 = 事件处理程序

    C，一个事件只能触发执行一次

    D，事件函数内this指的是当前触发事件的元素
```

答案: BD

解析: A选项，页面加载完只会触发页面加载事件；B选项，正确的注册事件方式；C选项，事件是触发一次执行一次；D选项，事件处理函数中this指向事件源对象；

## `7`- 操作元素内容

- 多选题

    关于操作元素的内容，说法正确的是：

```
    A，innerHTML可以识别渲染html标签

    B，innerText不可以识别html标签 

    C，element.innerHTML = ''; 和 element.innerText = ''; 作用一样

    D，var content = element.innerHTML; 和 var content = element.innerText; 的作用一样
```

答案：ABC

解析：innerText和innerHTML的区别。修改内容时,innerHTML可以识别渲染标签，innerText不可以，所有AB选项正确。C选项，都是清空标签的内容，正确。D选项，获取内容时，innerHTML会原封不动的获取内容包括标签、空白、换行，而innerText会过滤标签、空白、换行

## `8`- 操作元素属性

- 单选题

    关于操作元素的属性，错误的是：

```
    A，element.id = 'box01';

    B，element.src = 'image/new.jpg'; 

    C，element.title = '小菠萝';

    D，element.class = 'contentLeft';
```

答案：D

解析：操作元素常用属性。操作元素属性的格式为：元素对象.属性名 = 值; 但是class属性特殊，用className

## `9`- 循环精灵图背景

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        li {
            list-style: none;
        }
        .box {
            width: 250px;
            margin: 100px auto;
        }
        .box li {
            float: left;
            width: 24px;
            height: 24px;
            margin: 15px;
            background: url(images/sprite.png) no-repeat;
        }
    </style>
<body>
    <div class="box">
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
    <script>
        var lis = document.querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            // 让索引号 乘以 44 就是每个li 的背景y坐标  index就是我们的y坐标
            var index = i * 44;
            lis[i].style.backgroundPosition = '0 -' + index + 'px';
        }
    </script>
</body>
```

## `10`- 分时显示不同图片,显示不同问候语

- 题目描述

    1.根据不同时间，页面显示不同图片，同时显示不同的问候语

    2.如果上午时间打开页面，显示上午好，显示上午的图片

    3.如果下午时间打开页面，显示下午好，显示下午的图片

    4.如果晚上时间打开页面，显示晚上好，显示晚上的图片

```html
    <img src="images/s.gif" alt="">
    <div>上午好</div>
    <script>
        var img = document.querySelector('img');
        var div = document.querySelector('div');
        var date = new Date();
        var h = date.getHours();
        if (h < 12) {
            img.src = 'images/s.gif';
            div.innerHTML = '上午好';
        }   else if (h < 18) {
            img.src = 'images/x.gif';
            div.innerHTML = '下午好';
        }   else {
            img.src = 'images/w.gif';
            div.innerHTML = '晚上好';
        }
    </script>
```
