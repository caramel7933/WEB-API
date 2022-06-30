## `1`- 倒计时加强版

```html
<!DOCTYPE html>
<html lang="en">
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
        body {
            background-color: rgb(237, 237, 237);
        }
        .box {
            width: 800px;
            margin: 100px auto;
            text-align: center;
        }
        .box div {
            padding: 50px;
            text-align: center;
            font-size: 50px;
            font-weight: 700;
        }
        .box span {
            display: inline-block;
            width: 150px;
            height: 50px;
            padding: 30px 0;
            line-height: 50px;
            font-size: 50px;
            color: hotpink;
            text-align: center;
        }
        span:nth-of-type(n+2) {
            background-color: #717070;
        }
    </style>
</head>
<body>
    <div class="box">
        <div>距离恰饭时间还有————</div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
    </div>
    <script>
        var box = document.querySelector('.box');
        var inputTime = + new Date('2022-6-10 18:00:00');
        countDown();
        var times = setInterval(countDown,1000);
        function countDown() {
            var nowTime = + new Date();
            var Timer = (inputTime - nowTime) / 1000;
            var d = parseInt(Timer / 60 / 60 / 24);
            d = d < 10 ? '0' + d : d;
            var h = parseInt(Timer / 60 / 60 % 24);
            h = h < 10 ? '0' + h : h;
            var m = parseInt(Timer / 60 % 60);
            m = m < 10 ? '0' + m : m;
            var s = parseInt(Timer % 60);
            s = s < 10 ? '0' + s : s;
            if (Timer <= 0) {
                clearInterval(times);
                alert('时间到了');
                return false;
            }
            box.children[1].innerHTML = d + '天';
            box.children[2].innerHTML = h;
            box.children[3].innerHTML = m;
            box.children[4].innerHTML = s;
        }
    </script>
</body>
</html>
```

## `2`- 模态框拖拽

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
        a {
            text-decoration: none;
            color: #666;
        }
        .login-header {
            width: 100%;
            height: 30px;
            line-height: 30px;
            text-align: center;
            font-size: 24px;
        }
        .login {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            width: 512px;
            height: 280px;
            border: 1px solid #ebebeb;
            background-color: #fff;
            transform: translate(-50%, -50%);
            box-shadow: 0 2px 20px #ddd;
            z-index: 999;
        }
        .login-title {
            position: relative;
            width: 100%;
            height: 40px;
            margin-top: 10px;
            line-height: 40px;
            text-align: center;
            font-size: 18px;
            cursor: move;
        }
        .close-login {
            position: absolute;
            top: -30px;
            right: -20px;
            width: 40px;
            height: 40px;
            font-size: 12px;
            background-color: #fff;
            border: 1px solid #ebebeb;
            border-radius: 20px;
        }
        .login-input {
            overflow: hidden;
            margin-top: 20px;
        }
        .login-input label {
            float: left;
            width: 90px;
            height: 35px;
            padding-right: 10px;
            text-align: right;
            line-height: 35px;
            font-size: 14px;
        }
        .login-input input {
            float: left;
            width: 350px;
            height: 35px;
            line-height: 35px;
            text-indent: 5px;
            border: 1px solid #ebebeb;
        }
        .login-button {
            width: 50%;
            margin: 30px auto 0;
            line-height: 40px;
            text-align: center;
            font-size: 14px;
            border: 1px solid #ebebeb;
        }
        .login-button a {
            display: block;
        }
        .login-bg {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, .3);
        }
    </style>
</head>
<body>
    <div class="login-header">
        <a href="javascript:;" class="link">点击，弹出登录框</a>
    </div>
    <div class="login">
        <div class="login-title">
            登录会员
            <span>
                <a href="javascript:;" class="close-login">关闭</a>
            </span>
        </div>
        <div class="login-con">
            <div class="login-input">
                <label for="username">用户名：</label>
                <input type="text" placeholder="请输入用户名" id = "username"><br>
            </div>
            <div class="login-input">
                <label for="password">密码：</label>
                <input type="text" placeholder="请输入登录密码" id="password">
            </div>
        </div>
        <div class="login-button">
            <a href="javascript:;">登录</a>
        </div>
    </div>
    <div class="login-bg"></div>
    <script>
        var link = document.querySelector('.link');
        var login = document.querySelector('.login');
        var close = document.querySelector('.close-login');
        var bg = document.querySelector('.login-bg');
        var title = document.querySelector('.login-title');
        link.addEventListener('click', function() {
            login.style.display = 'block';
            bg.style.display = 'block';
        })
        close.addEventListener('click', function() {
            login.style.display = 'none';
            bg.style.display = 'none';
        })
        title.addEventListener('mousedown', function(e) {
            var x = e.pageX - login.offsetLeft;
            var y = e.pageY - login.offsetTop;
            document.addEventListener('mousemove', move);
            function move(e) {
                login.style.left = e.pageX - x + 'px';
                login.style.top = e.pageY - y + 'px';
            }
            document.addEventListener('mouseup', function() {
                document.removeEventListener('mousemove', move);
            })
        })
    </script>
</body>
```

## `3`- 仿固定侧边栏

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
        .w {
            width: 1200px;
            margin: 10px auto;
        }
        .slider_bar {
            position: absolute;
            top: 300px;
            left: 50%;
            width: 45px;
            height: 130px;
            margin-left: 620px;
            background: darkgrey;
        }
        .slider_bar span {
            margin-top: 80px;
            cursor: pointer;
        }
        .header {
            height: 150px;
            background: blanchedalmond;
        }
        .banner {
            height: 250px;
            background: palevioletred;
        }
        .main {
            height: 1000px;
            background: salmon;
        }
        .goBack {
            display: none;
        }
    </style>
</head>
<body>
    <div class="slider_bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体部分</div>
    <script>
        var slider_bar = document.querySelector('.slider_bar');
        var banner = document.querySelector('.banner');
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');
        // banner.offestTop 就是被卷去头部的大小 一定要写到滚动的外面
        var bannerTop = banner.offsetTop;
        var mainTop = main.offsetTop;
        var sliderbarTop = slider_bar.offsetTop - bannerTop;
        document.addEventListener('scroll', function() {
            if (window.pageYOffset >= bannerTop) {
                slider_bar.style.position = 'fixed';
                slider_bar.style.top = sliderbarTop + 'px';
            } else {
                slider_bar.style.position = 'absolute';
                slider_bar.style.top = '300px';
            }
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }
        })
        goBack.addEventListener('click', function() {
            // 因为是窗口滚动，所以用window
            animate(window, 0);
        })
        // 动画函数
        function animate(obj, target, callback) {
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                var step = (target - window.pageYOffset) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (window.pageYOffset == target) {
                    clearInterval(obj.timer);
                    callback && callback();
                } else {
                    window.scroll(0, window.pageYOffset + step);
                }
            }, 15)
        }
    </script>
</body>
```

## `4`- offset系列属性

- 单选题

    以下关于offset系列属性和style属性的说法，正确的是()
```
    A.通过style属性获取到的样式结果是字符串类型，而通过offset系列获取到的属性值是数字类型

    B.offset系列属性和style属性一样，都可以获取到元素的行内样式

    C.style系列属性只能获取元素的行内样式，offset系列属性能获取到元素的所有样式

    D.以上说法都不正确
```

答案: A

解析: 本题考查的是 offset 系列属性的使用。答案B和C错误，offset系列属性用来获取元素显示的效果，但是并不是所有的样式都能够获取到，只能获取到宽度，高度，左右距离等

- 单选题

    下列关于offsetWidth和offsetHeight的说法，正确的是()

```
    A.这两个属性用来表示内容的大小，不包括边框和内边距

    B.获取到结果是数字类型，方便计算。计算完成以后的值，可以再使用offsetWidth和offsetHeight重新设置给元素

    C.这两个属性值的结果是字符串类型的数据，默认单位是px

    D.这两个属性是只读属性
```

答案: D

解析: 本题考查的是 offset 系列属性的使用。答案A错误，offsetWidth和offsetHeight表示的是盒子的大小，包括边框和内边距；答案B错误，这两个属性是只读属性，不能被修改；答案C错误，这两个属性获取到的结果是数字类型，不是字符串类型

- 多选题

    下列关于offsetParent的说法，正确的是()

```
    A.offsetParent 获取到的是元素的父元素

    B.offsetParent 属性和 parentNode属性的含义一样

    C.offsetParent属性用来获取离这个元素最近的绝对定位父元素

    D.以上说法都错误
```

答案: AB

解析: 本题考查的是 offset 系列属性的使用。答案C错误，offsetParent获取的是离这个元素最近的有定位的父元素，不管这个父元素是绝对定位还是相对定位。所以A和B也错误

## `5`- scroll系列属性的使用

- 多选题

    以下关于touch事件说法正确的是（）

```
    A.click是鼠标事件，但是在移动端也能使用

    B.mousedown和mouseup是鼠标事件，在移动端能够使用

    C.鼠标事件click在移动端比touchstart执行效率高

    D.鼠标事件在移动端不能够使用

    E.在移动端，touch事件比鼠标事件执行效率高
```

答案: ABE

解析: 本题考查的是touch事件和鼠标事件在移动端的区别。答案C错误，在移动端touch相关的事件类型比鼠标事件执行效率高；答案D错误，鼠标事件在移动端也可以使用

- 多选题

    以下关于scroll系列属性的说法正确的是()

```
    A.scrollWidth和scrollHeight获取的是盒子的大小，包括边框和内边距

    B.scrollTop 指的是盒子内容被滚动条卷去的头部的高度

    C.scroll系列属性和offset系列属性的作用一样

    D.scrollParent属性用来获取滚动时参考的父元素
```

答案：B

解析：本题考查的是scroll属性的使用。答案A错误，scrollWidth和scrollHeight获取到的是内容的大小；答案C错误，scroll系列和offset系列属性的作用不一样；答案D错误，没有scrollParent这个属性

- 多选题

    以下关于scroll系列属性的说法错误的是()

```
    A.一般情况下，我们不会获取某一个元素的滚动距离，通常会获取整个页面的滚动距离。

    B.监听一个元素的滚动，需要给这个元素添加onscroll事件

    C.获取页面的滚动距离，document.documentElement.scrollTop 和 document.body.scrollTop;

    D.scrollRight获取的是盒子内容被滚动条卷去的右边的宽度
```

答案：CD

解析：本题考查的是scroll属性的使用。答案C错误，获取页面的滚动距离用 window.pageYOffset 或者 window.pageXOffset ;答案D错误，没有scrollRight这个属性

## `6`- 记住用户名

如果勾选记住用户名， 下次用户打开浏览器，就在文本框里面自动显示上次登录的用户名

```html
<body>
    <input type="text" id="username"> <input type="checkbox" id="remember">记住用户名
    <script>
        var username = document.querySelector('#username');
        var rem = document.querySelector('#remember');
        if (localStorage.getItem('username')) {
            username.value = localStorage.getItem('username');
            rem.checked = true;
        }
        rem.addEventListener('change', function() {
            if (this.checked) {
                localStorage.setItem('username', username.value);
            } else {
                localStorage.remove('username');
            }
        })
    </script>
</body>
```

## `7`- touchEvent

- 单选题

    以下哪些不属于touch事件对象的属性（）

```
    A.changedTouches属性

    B.targetTouches属性

    C.touches属性

    D.touch属性
```

答案: D

解析: 本题考查的是touchEvent中常见的属性。答案D错误，因为没有这个属性

- 多选题

    以下关于touch事件对象说法正确的是（）

```
    A.touches属性可以获取屏幕上的所有手指的列表

    B.changedTouches属性在touchend事件处理程序中得到改变的手指列表

    C.targetTouches属性和touches在手指按下和移动中都可以获取手指列表

    D.手指列表中的某一个手指的clientX和pageX在移动端可以互相使用

    E.在click事件中也可以获取touches属性
```

答案：ABCD

解析：本题考查的是touchEvent创建的属性及作用。答案E错误，鼠标事件中不存在touches属性

## `8`- touch事件类型

- 单选题

    以下关于touch事件说法错误的是（）

```
    A.touchstart是指手指按压下去后触发

    B.touchmove是手指按压并且滑动后触发

    C.touchend是手指松开后触发

    D.touchover是指手指松开后触发
```

答案: D

解析: 本题考查的是touch相关的事件类型。答案D错误，因为没有这个事件