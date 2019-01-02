---
title: 如何使用fonts.googleapis.com使自己的网站增加更多字体
date: 2019-01-02 17:04:17
tags: 
    - googleapis
    - 字体
categories: HTML
---
首先，fonts.googleapis.com解决的是客户端电脑没有安装字体，但是网站主又想客户看到自己想要的字体，通常的做法就是网站的css调用网站内部的字体文件，但是这样做非常不灵活，我们需要更换字体时，不然需要修改css，还需要替换字体文件，于是fonts.googleapis.com就可以解决这个问题。
<!--more-->
# 使用方法
CSS引入
```CSS
 <link href="//fonts.googleapis.com/css?family=Monda:300,300italic,400,400italic,700,700italic|PT Mono:300,300italic,400,400italic,700,700italic&subset=latin,latin-ext" rel="stylesheet" type="text/css">
```
链接的具体构成就是：
fonts.googleapis.com/css?family=**字体名称**:**加粗程度**,**加粗程度+是否斜体**&subset=latin,latin-ext
其中如果需要多种字体用  **|**  隔开，如果有多种加粗程度
最后在需要使用的元素上加入font-family属性即可
```html
body {
    font-family: 'Monda', 'PT Mono' , serif;
    font-size: 48px;
}
```

> fonts.googleapis.com还有一种ajax请求方式，这里不推荐使用，css是最快也最容易维护的方式。
