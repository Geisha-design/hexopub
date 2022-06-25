---
layout: post
title: 基于DOM的Web信息提取方法
date: 2022-05-06 13:06:06
tags:

---





文章目录
一、什么是DOM？
DOM树：
1.文档：
2.元素：
3.节点：
二、获取页面中的元素的几种方法：
1.根据 id 获取元素
2.根据标签名获取元素
3.通过HTML5新增的方法获取元素
4.根据特殊元素获取元素
一、什么是DOM？
DOM简称：文档对象模型，是一种处理可扩展编程语言的标准编程接口，我们通过这些接口来改变网页的内容、结构和样式。<!--more-->

DOM树：


1.文档：
一个网页就是一个文档，DOM中使用document表示

2.元素：
页面中的所有标签都是元素，DOM中使用element表示

3.节点：
网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示

二、获取页面中的元素的几种方法：
1.根据 id 获取
2.根据标签名获取
3.通过HTML5新增的方法获取
4.特殊元素获取

1.根据 id 获取元素
这里我们讲通过使用getElementByld根据id获取页面元素：

getElementByld语法： var element = doucument.getElementByld(id);
参数：element是一个Element对象，如果当前文档中拥有特定ID的元素不存在则返回null
     id是大小写敏感的字符串，代表了所要查找元素的唯一ID
返回值：返回一个匹配到 ID 的 DOM Element对象。若在当前Document下没有找到，则返回null
1
2
3
4
代码如下（示例）：

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div id="time">2022-3-2</div>
        <script>
            var timer = document.getElementById('time');
            console.log(timer);
            console.log(typeof timer);/*返回的是一个元素对象*/
        </script>
    </body>
</html>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
运行结果：

我们可以看到返回的类型是对象类型，这就更能体现出DOM是一个文档对象模型了

2.根据标签名获取元素
<ul>
            <li>噜啦啦噜啦啦，啦啦啦啦啦</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦</li>
</ul>
1
2
3
4
5
6
7
如果我们想获取这五个li对象应该怎么做呢，这个时候根据id获取是不是很麻烦，所以这时候就用到了我们的根据标签名获取元素的getElementsByTagName()方法

代码如下所示：

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li>噜啦啦噜啦啦，啦啦啦啦啦1</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦2</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦3</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦4</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦5</li>
        </ul>
        <script>
            var lis = document.getElementsByTagName('li');
            console.log(lis);
        </script>
    </body>
</html>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
运行结果：

getElementsByTagName返回的是获取过来元素对象的集合，以伪数组的形式存储的


如果我们想获取第一个li里面的元素可以通过数组形式访问：
console.log(lis[0]);

如果想要依次打印里面的元素对象我们可以采取遍历的方式：
for( var i = 0; i < lis.length; i++)
{
    console.log(lis[i]);
}
1
2
3
4
5
6
7
8
9
注意：
1.因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历。
2.得到元素对象是动态的

<ul>
            <li>噜啦啦噜啦啦，啦啦啦啦啦1</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦2</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦3</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦4</li>
            <li>噜啦啦噜啦啦，啦啦啦啦啦5</li>
</ul>
<ol>
            <li>哇哇哇哇哇哇哇哇</li>
            <li>哇哇哇哇哇哇哇哇</li>
            <li>哇哇哇哇哇哇哇哇</li>
            <li>哇哇哇哇哇哇哇哇</li>
</ol>
1
2
3
4
5
6
7
8
9
10
11
12
13
那如果我们的代码是这样的。我们想获取ol 里面的 li 该怎么办。
那我们就不可以用document.getElementsByTagName()来获取对象了，因为这样会把我们页面里的所有 li 都获取出来。

这时候我们可以通过这个方法获取某个元素（父元素）内部所有指定标签名的子元素

element.getElementsByTagName('标签名');
1
注意：父元素必须是单个对象（必须指明是哪一个元素对象）.获取的时候不包括父元素自己

我们可以这样做：

var ol = document.getElementsByTagName('ol');  //[ol],得到的是一个伪数组，所以父元素应该是ol[0]
console.log(ol[0].getElementsByTagName('li'));
1
2
也可以这样做：
为了方便我们给ol 标签加一个id属性：

<ol id = "ol">
1
var ol = document.getElementById('ol');//这样我们就直接获取到了父元素
console.log(ol.getElementsByTagName('li'));
1
2
3.通过HTML5新增的方法获取元素
这个是HTML5新增的获取元素的方法

document.getElementsByClassName('类名'); //根据类名返回元素对象集合
1
示例代码如下：

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div class="box">盒子1</div>
        <div class="box">盒子2</div>
        <div class="nav">
            <ul>
                <li>首页</li>
                <li>产品</li>
            </ul>
        </div>
        <script>
            var boxs = document.getElementsByClassName('box');
            console.log(boxs);
        </script>
    </body>
</html>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
返回的对象也是以伪数组的形式存储的


这个同样也是HTML5新增的，而且功能非常强大

document.querySelector('选择器');  //根据指定选择器返回第一个元素对象
1
代码示例：

<script>
            var fisrtbox = document.querySelector('.box');
            console.log(fisrtbox);
            var nav = document.querySelector('#nav');//＃用于id选择器
            console.log(nav);
            var li = document.querySelector('li');
            console.log(li);
</script>
1
2
3
4
5
6
7
8
注意： querySelector 返回指定选择器的第一个元素对象，切记里面的选择器需要加符号

还有querySelectorAll方法

document.querySelectorAll('选择器');  //根据指定选择器返回
1
querySelectorAll返回的是指定选择器的所有元素对象集合

代码示例:

<script>
            var allbox = document.querySelectorAll('.box');
            console.log(allbox);
 </script>
1
2
3
4
运行结果：

如果不考虑兼容性的话，推荐使用querySelector和querySelectorAll来获取元素

4.根据特殊元素获取元素
如果我们想获取页面中的body 元素，和html元素应该怎么办呢？
大家看以下代码：

<script>
            //获取body元素
            var bodyELE = document.body;
            console.log(bodyELE);
            //获取html元素
            var htmlELE = document.documentElement;
            console.log(htmlELE);
 </script>
1
2
3
4
5
6
7
8
运行结果：

那么以下就是获取特殊元素（body,html）的语法：

1.document.body  //返回body元素对象
2.document.documentElement  //返回html元素对象

