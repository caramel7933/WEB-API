## `1`- 添加表格内容

- 题目描述

    用户在页面上点击按钮,可以把文本框中的数据在表格的新的一行中显示

```html
    <style>
        table {
            width: 600px;
            margin-top: 30px;
            cursor: pointer;
            border-collapse: collapse;
        }
        table td {
            text-align: center;
        }
        table th {
            background-color: blueviolet;
        }
        table td {
            background-color: #eee;
        }
    </style>
</head>
<body>
    <div id="dv">
        请输入姓名:
        <input type="text" value="" id="uname">
        <br> 请输入邮箱:
        <input type="text" value="" id="email">
    </div>
    <input type="button" value="添加" id="btn">
    <table id="tb">
        <thead>
            <tr>
                <th>姓名</th>
                <th>邮箱</th>
            </tr>
        </thead>
        <tbody id="tbd">
            <tr>
                <td>小黑</td>
                <td>xiaohei@126.com</td>
            </tr>
        </tbody>
    </table>
    <script>
        var btn = document.getElementById('btn');
        var uname = document.getElementById('uname');
        var email = document.getElementById('email');
        var tbd = document.getElementById('tbd');
        // 获取按钮注册点击事件
        btn.onclick = function() {
            if (uname.value == '' || email.value == '') {
                alert('请完善所有信息');
                return;
            }
            // 创建一行
            var trObj = document.createElement('tr');
            // 把行加入到tbody中
            tbd.appendChild(trObj);
            var td1 = document.createElement('td');
            td1.innerHTML = uname.value;
            var td2 = document.createElement('td');
            td2.innerHTML = email.value;
            trObj.appendChild(td1);
            trObj.appendChild(td2);
        }
    </script>
```

## `2`- 简单版发布留言

```html
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        body {
            padding: 100px;
        }
        textarea {
            width: 200px;
            height: 100px;
            border: 2px solid rgb(213, 127, 141);
            outline: none;
            resize: none;
        }
        ul {
            margin-top: 50px;
        }
        li {
            width: 300px;
            padding: 5px;
            background-color: skyblue;
            color: blueviolet;
            font-size: 14px;
            margin: 15px 0;
        }
    </style>
</head>
<body>
    <textarea name="" id="" cols="30" rows="10"></textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        var text = document.querySelector('textarea');
        var btn = document.querySelector('button');
        var ul = document.querySelector('ul');
        btn.onclick = function() {
            if (text.value == '') {
                alert('您还没有输入内容哦');
                return false;
            }
            var li = document.createElement('li');
            li.innerHTML = text.value;
            ul.insertBefore(li, ul.children[0]);
        }
    </script>
</body>
```

## `3`- tab 栏切换

当鼠标点击上面相应的选项卡（tab），下面内容跟随变化

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
        .wrap {
            width: 978px;
            margin: 100px auto;
        }
        .tab_list {
            height: 39px;
            border: 1px solid #ccc;
            background-color: #f1f1f1;
        }
        .tab_list li {
            float: left;
            height: 39px;
            line-height: 39px;
            padding: 0 30px;
            text-align: center;
            cursor: pointer;
        }
        .tab_list .current {
            background-color: #c81623;
            color: #fff;
        }
        .item {
            display: none;
        }
    </style>
</head>
<body>
    <div class="wrap">
        <div class="tab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价(50000)</li>
                <li>手机社区</li>
            </ul>
        </div>
        <div class="tab_con">
            <div class="item" style="display: block;">
                商品介绍模块内容
            </div>
            <div class="item">
                规格与包装模块内容
            </div>
            <div class="item">
                售后保障模块内容
            </div>
            <div class="item">
                商品评价(50000)模块内容
            </div>
            <div class="item">
                手机社区模块内容
            </div>
        </div>
        <script>
            var lis = document.querySelector('.tab_list').querySelectorAll('li');
            var items = document.querySelectorAll('.item');
            for (var i = 0; i < lis.length; i++) {
                lis[i].setAttribute('index', i);
                lis[i].onclick = function() {
                    for (var i = 0; i < lis.length; i++) {
                        lis[i].className = '';
                    }
                    this.className = 'current';
                    var index = this.getAttribute('index');
                    // 干掉所有人 让其余的item 这些div 隐藏
                    for (var j = 0; j < items.length; j++) {
                        items[j].style.display = 'none';
                    }
                    // 留下我自己 让对应的item 显示出来
                    items[index].style.display = 'block';
                }
            }
        </script>
    </div>
</body>
```

## `4`- 表单全选取消全选

题目要求：

1. 点击上面全选复选框，下面所有的复选框都选中（全选）

2. 再次点击全选复选框，下面所有的复选框都不选中（取消全选）

3. 如果下面复选框全部选中，上面全选按钮就自动选中

4. 如果下面复选框有一个没有选中，上面全选按钮就不选中

5. 所有复选框一开始默认都没选中状态

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
        .wrap {
            width: 300px;
            margin: 100px auto;
        }
        table {
            width: 300px;
            border: 1px solid #c0c0c0;
            border-collapse: collapse;
        }
        th,td {
            color: #404060;
            padding: 10px 0;
            text-align: center;
            border: 1px solid #d0d0d0;
        }
        th {
            background-color: skyblue;
        }
        td {
            cursor: pointer;
        }
        .b-check tr:hover {
            background-color: aliceblue;
        }
        .b-check {
            background-color: #fcfcfc;
        }
    </style>
</head>
<body>
    <div class="wrap">
        <table>
            <thead>
                <tr>
                    <th>
                        <input type="checkbox" id="h-check">
                    </th>
                    <th>商品</th>
                    <th>价钱</th>
                </tr>
            </thead>
            <tbody class="b-check">
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPad Pro</td>
                    <td>5000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPad Air</td>
                    <td>2000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>Apple Watch</td>
                    <td>2000</td>
                </tr>
            </tbody>
        </table>
    </div>
    <script>
        var hcheck = document.getElementById('h-check');
        var bcheck = document.querySelector('.b-check').querySelectorAll('input');
        hcheck.onclick = function() {
            // this.checked 它可以得到当前复选框的选中状态如果是true 就是选中，如果是false 就是未选中
            for (var i = 0; i < bcheck.length; i++) {
                bcheck[i].checked = this.checked;
            }
        }
        // 给下面所有复选框绑定点击事件，每次点击，都要循环查看下面所有的复选框是否有没选中，如果有一个没选中的， 上面全选就不选中
        for (var i = 0; i < bcheck.length; i++) {
            bcheck[i].onclick = function() {
                // 每次点击下面的复选框都要循环检查这4个小按钮是否全被选中
                for (var i = 0; i < bcheck.length; i++) {
                    var flag = true;
                    if ( !bcheck[i].checked)  {
                        flag = false;
                        break;  // 退出for循环 这样可以提高执行效率 因为只要有一个没有选中，剩下的就无需循环判断了
                    }
                }
                hcheck.checked = flag;
            }
        }
    </script>
</body>
```

## `5`- 表格隔行变色

```html
    <style>
        table {
            width: 800px;
            margin: 100px auto;
            text-align: center;
            font-size: 14px;
            border-collapse: collapse;
        }
        thead tr {
            height: 30px;
            background-color: skyblue;
        }
        tbody tr {
            height: 30px;
        }
        tbody td {
            border-bottom: 1px solid #d7d7d7;
            font-size: 12px;
            color: blue;
            cursor: pointer;
        }
        .bg {
            background-color: yellowgreen;
        }
    </style>
<body>
    <table>
        <thead>
            <tr>
                <th>代码</th>
                <th>名称</th>
                <th>最新公布净值</th>
                <th>累计净值</th>
                <th>前单位净值</th>
                <th>净值增长率</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
        </tbody>
    </table>
    <script>
        var trs = document.querySelector('tbody').querySelectorAll('tr');
        for (var i = 0; i < trs.length; i++) {
            trs[i].onmouseover = function() {
                this.className = 'bg';
            }
            trs[i].onmouseout = function() {
                this.className = '';
            }
        }
    </script>
</body>
```

## `6`- 换肤效果

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        body {
            background: url(images/1.jpg) no-repeat center top;
        }
        li {
            list-style: none;
        }
        .baidu {
            overflow: hidden;       
            width: 410px;
            margin: 100px auto;
            padding-top: 3px;
            background-color: #fff;
        }
        .baidu li {
            float: left;
            margin: 0 1px;
            cursor: pointer;
        }
        .baidu img {
            width: 100px;
        }
    </style>
<body>
    <ul class="baidu">
        <li>
            <img src="images/1.jpg" alt="">
        </li>
        <li>
            <img src="images/2.jpg" alt="">
        </li>
        <li>
            <img src="images/3.jpg" alt="">
        </li>
        <li>
            <img src="images/4.jpg" alt="">
        </li>
    </ul>
    <script>
        var imgs = document.querySelector('.baidu').querySelectorAll('img');
        for (var i = 0; i < imgs.length; i++) {
            imgs[i].onclick = function() {
                document.body.style.backgroundImage = 'url(' + this.src + ')';
            }
        }
    </script>
</body>
```

## `7`- 操作自定义属性

- 单选题

    关于操作元素的class属性，正确的是：
```
    A，element.setAttribute('className', 'active');

    B，element.class = 'active'; 

    C，element.className = 'active';

    D，element.class-name = 'active';
```

答案：c

解析：操作元素属性的格式为：元素对象.属性名 = 值; 但是class属性特殊，用className。使用setAttribute操作class时用class

- 多选题

    有一标签`<div data-uname="ls"></div>` ，可以获取标签自定义属性的选项是：

```
    A，divObj.dataset["uname"]

    B，divObj.dataset.uname 

    C，divObj.getAttribute('data-uname')

    D，divObj.data-uname
```

答案：ABC

解析：

1.兼容性获取 `element.getAttribute(‘data-index’); ` 

2.H5新增 ` element.dataset.index;`  

3.或者 ` element.dataset['index'];`

## `8`- 节点的层级关系

- 单选题

    关于节点操作，下面选项能获取子元素节点的是：

```
    A，element.child

    B，element.childNode

    C，element.childNodes

    D，element.children
```

答案：D

解析：获取子节点使用childNodes，获取子元素节点使用children

- 多选题

    关于节点的层级关系操作，下面描述正确的是：

```
    A，使用子节点.parentNode可以找到父节点

    B，使用父节点.children 找到所有的子元素

    C，使用父节点.children 找到所有的子节点

    D，使用节点.parentNode.parentNode可以找到父节点的父节点
```

答案：ABD

解析：节点之间的层级关系，获取父节点使用parentNode，获取子节点使用childNodes，获取子元素children

## `9`- 动态生成表格

```html
<style>
        table {
            width: 500px;
            margin: 100px auto;
            text-align: center;
            border-collapse: collapse;
        }
        th,td {
            border: 1px solid #333;
        }
        thead tr {
            height: 40px;
            background-color: #ccc;
        }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>姓名</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>

        </tbody>
    </table>
    <script>
        var datas = [{
            name: '瓦1',
            subject: 'JavaScript',
            score: 100
        }, {
            name: '瓦2',
            subject: 'JavaScript',
            score: 99
        }, {
            name: '瓦3',
            subject: 'JavaScript',
            score: 88
        }, {
            name: '瓦4',
            subject: 'JavaScript',
            score: 80
        }];
        var tbody = document.querySelector('tbody');
        for (var i = 0; i < datas.length; i++) {
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            for (var k in datas[i]) {
                var td = document.createElement('td');
                // 把对象里面的属性值 datas[i][k] 给 td  
                td.innerHTML = datas[i][k];
                tr.appendChild(td);
            }
            var td = document.createElement('td');
            td.innerHTML = "<a href='javascript:;'>删除</a>";
            tr.appendChild(td);
        }
        var as = document.querySelectorAll('a');
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function() {
                tbody.removeChild(this.parentNode.parentNode);
            }
        }
        // for(var k in obj) {
        //     k 得到的是属性名
        //     obj[k] 得到是属性值
        // }
    </script>
</body>
```

## `10`- 删除留言板内容

```html
<style>
        * {
            padding: 0;
            margin: 0;
        }
        body {
            padding: 100px;
        }
        textarea {
            width: 200px;
            height: 100px;
            border: 1px solid pink;
            outline: none;
            resize: none;
        }
        ul {
            margin-top: 50px;
        }
        li {
            width: 300px;
            padding: 5px;
            background-color: #eee;
            color: blueviolet;
            font-size: 14px;
            margin: 15px 0;
        }
        li a {
            text-decoration: none;
            float: right;
            color: #666;
        }
    </style>
</head>
<body>
    <textarea name="" id="" cols="30" rows="10"></textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('请输入内容');
                return;
            }
            // (1) 创建元素
            var li = document.createElement('li');
            // 先有li 才能赋值
            //阻止链接跳转需要添加 javascript:void(0); 或者 javascript:;
            li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";
            // (2) 添加元素
            ul.insertBefore(li, ul.children[0]);
            // (3) 删除元素 删除的是当前链接的li  它的父亲
            var as = document.querySelectorAll('a');
            for (var i = 0; i < as.length; i++) {
                as[i].onclick = function() {
                    // node.removeChild(child); 删除的是 li 当前a所在的li  this.parentNode;
                    ul.removeChild(this.parentNode);
                }
            }
        }
    </script>
</body>
```