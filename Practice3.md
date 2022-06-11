## `1`- 跟随鼠标的天使

这个天使图片一直跟随鼠标移动

`核心原理`： 每次鼠标移动，我们都会获得最新的鼠标坐标， 把这个x和y坐标做为图片的top和left 值就可以移动图片

```html
    <style>
        img {
            position: absolute;
        }
    </style>
</head>
<body>
    <img src="images/angel.gif" alt="">
    <script>
        var img = document.querySelector('img');
        document.addEventListener('mousemove', function(e) {
            var x = e.pageX;
            var y = e.pageY;
            img.style.top = y - 40 + 'px';
            img.style.left = x - 50 + 'px';
        })
    </script>
```

## `2`- 动态添加列表

- 题目描述

    页面上有一些美女列表，当单击li时背景色变为红色，但点击按钮时会新增1个美女到列表最前面，并且单击新增的美女背景也会变为红色

```html
<body>
    <ul>
        <li>西施</li>
        <li>貂蝉</li>
        <li>昭君</li>
        <li>凤姐</li>
        <li>芙蓉姐姐</li>
    </ul>
    <input type="button" value="按钮" id="btn">
    <script>
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            e.target.style.backgroundColor = 'pink';
        })
        var btn = document.getElementById('btn');
        btn.onclick = function() {
            var liObj = document.createElement('li');
            liObj.innerHTML = '杨超越';
            ul.insertBefore(liObj, ul.children[0]);
        }
    </script>
</body>
```

## `3`- 创建添加元素

- 多选题

    下列哪些选项可以实现创建元素：

```
    A，element.push('<p>小菠萝</p>')

    B，element.pop('<p>小菠萝</p>');

    C，element.innerHTML = '<p>小菠萝</p>';

    D，document.createElement("p")';
```

答案：CD

解析：创建元素的方法

- 多选题

    关于添加元素，下列选项描述正确的是：

```
    A，innerHTML会覆盖原来的元素

    B，appendChild 是在父元素内部追加

    C，insertBefore 可以在父元素内部指定的位置添加

    D， createElement创建的元素立即会添加在页面
```

答案：ABC

解析：创建添加元素的方法，D选项，createElement要配合其他添加方法使用

## `4`- 事件监听

- 多选题

    关于事件监听，描述正确的是：

```
    A，可以给同一元素同一事件注册多个监听器

    B，addEventListener() 有浏览器兼容问题 

    C，addEventListener() 方法有3个参数

    D，低版本的IE可以使用attachEvent代替addEventListener
```

答案：ABCD

解析：IE9以后才支持addEventListener，低版本IE使用attachEvent

## `5`- 事件对象

- 多选题

`关于事件对象，描述正确的是：

```
    A，事件对象的属性中保存了跟事件相关的一系列信息

    B，事件触发时就会产生事件对象

    C，事件对象的获取有兼容性问题

    D，通过事件对象可以阻止事件冒泡和默认行为
```

答案：ABCD

解析：事件对象有很多方法和属性，保存了事件相关的信息，获取时有兼容性问题，使用事件对象可以阻止事件冒泡和默认行为

- 单选题

    下列选项，哪个可以正确获取到兼容了各个浏览器的事件对象：

```
    A，document.onclick = function(evt){  var e=window.event||event;  };

    B，document.onclick  = function(evt){  var e=window.evt||event;  };

    C，document.onclick  = function(evt){  var e=window.event||evt;  };

    D，document.onclick  = function(evt){  var e=window.evt||evt;  };
```

答案：C

解析：事件对象的兼容性考虑。低版本的IE，通过 window.event获取事件对象

## `6`- 模拟京东快递单号查询

`要求`：当我们在文本框中输入内容时，文本框上面自动显示大字号的内容

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        .search {
            position: relative;
            width: 200px;
            margin: 150px;
        }
        .con {
            display: none;
            position: absolute;
            top: -40px;
            width: 170px;
            padding: 5px 0;
            border: 1px solid #ccc;
            box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
            font-size: 18px;
            color: #333;
        }
        .con::before {
            content: '';
            position: absolute;
            top: 28px;
            left: 18px;
            width: 0;
            height: 0;
            border: 8px solid #ccc;
            border-color: #fff transparent transparent;
        }
        .jd {
            outline: none;
        }
    </style>
</head>
<body>
    <div class="search">
        <div class="con"></div>
        <input type="text" placeholder="请输入快递单号" class="jd">
    </div>
    <script>
        var con = document.querySelector('.con');
        var jd_input = document.querySelector('.jd');
        document.addEventListener('keyup', function(e) {
            if (e.keyCode === 83) {
                jd_input.focus();
            }
        })
        jd_input.addEventListener('keyup', function() {
            if (this.value == '') {
                con.style.display = 'none';
            } else {
                con.style.display = 'block';
                con.innerHTML = this.value;
            }
        })
        jd_input.addEventListener('focus', function() {
            if (this.value !== '') {
                con.style.display = 'block';
            }   else {
                con.style.display = 'none';
            }
        })
        jd_input.addEventListener('blur', function() {
            con.style.display = 'none';
        })
    </script>
</body>
```

## `7`- 时钟

要求：做一个电子时钟，显示当前的年月日，时分秒，要求自动变化

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            background-color: rgb(171, 136, 189);
        }
        div {
            width: 700px;
            height: 300px;
            line-height: 300px;
            text-align: center;
            box-shadow: 0 2px 4px rgba(72, 44, 44, 0.2);
            border-radius: 15px;
            margin: 100px auto;
            background-color: plum;
            font-size: 30px;
            color: #fff;
        }
    </style>
</head>
<body>
    <div></div>
    <script>
        // 获取元素
        var div = document.querySelector('div');
        getTime();  // 提前调用一次函数，防止刷新有时间间隔
        // 使用定时器每隔1秒更新一次时间
        setInterval(getTime, 1000);
        // 封装时间函数，利用时间对象获取系统当前时间
        function getTime() {
            var date = new Date();
            var getFull = date.getFullYear();
            var mon = date.getMonth() + 1;
            var dates = date.getDate();
            var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            var day = date.getDay();
            var h = date.getHours();
            h = h < 10 ? '0' + h : h;
            var m = date.getMinutes();
            m = m < 10 ? '0' + m : m;
            var s = date.getSeconds();
            s = s < 10 ? '0' + s : s;
            div.innerHTML = getFull + '年' + mon + '月' + dates + '日 ' + arr[day] + ' ' +  h + ':' + m + ':' + s;
        }
    </script>
</body>
```
## `8`- 发送短信

点击按钮后，该按钮60秒之内不能再次点击，防止重复发送短信

```html
手机号码：<input type="text"> <button>发送</button>
    <script>
        var btn = document.querySelector('button');
        var time = 3;
        btn.addEventListener('click', function() {
            btn.disabled = true;
            var timer = setInterval(function() {
                if (time == 0) {
                    clearInterval(timer);
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                    time = 3;
                } else {
                    btn.innerHTML = '还剩下' + time + '秒';
                    time--;
                }
            }, 1000);
        })
    </script>
```

## `9`- 倒计时

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            margin: 200px;
        }
        span {
            display: inline-block;
            width: 40px;
            height: 40px;
            line-height: 40px;
            background-color: #333;
            color: #fff;
            text-align: center;
        }
    </style>
</head>
<body>
    <div>
        <span class="hour"></span>
        <span class="minute"></span>
        <span class="second"></span>
    </div>
    <script>
        var hour = document.querySelector('.hour');
        var minute = document.querySelector('.minute');
        var second = document.querySelector('.second');
        var inputTime = +new Date('2022-6-2 16:00:00');
        countDown();
        setInterval(countDown, 1000);
        function countDown() {
            var nowTime = +new Date();
            var Timer = (inputTime - nowTime) / 1000;
            var h = parseInt(Timer / 60 / 60 % 24);
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h;
            var m = parseInt(Timer / 60 % 60);
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;
            var s = parseInt(Timer % 60);
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;
        }
    </script>
</body>
</html>
```

## `10`- 5秒钟之后自动跳转页面

```html
<body>
    <button>点击</button>
    <div></div>
    <script>
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        var timer = 5;
        btn.addEventListener('click', function() {
            countDown();
            setInterval(countDown, 1000);
        })
        function countDown() {
            if (timer == 0) {
                location.href = 'http://www.baidu.com';
            } else {
                div.innerHTML = '您将在' + timer + '秒后跳转至首页';
                timer--;
            }
        }
    </script>
</body>
```