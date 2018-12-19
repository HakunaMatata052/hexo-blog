---
title: 无js实现选项卡效果
date: 2018-12-19 14:52:35
tags: [选项卡,无js]
categories: "HTML"
---

### 无js实现选项卡效果

## 方法一
# 效果展示
[点击查看效果](/dome1/)

# 实现原理
利用锚链接和滚动条实现

# 缺点
基本功能可以满足，但有两个问题，一是由于改变location的hash实现的定位，会触发浏览器原生滚动行为，体验不好；二是选项卡内容的切换“邦邦邦”过于生硬
<!-- more -->
# 具体代码
## HTML
```HTML
<div class="box">
	<div class="list" id="one">1</div>
    <div class="list" id="two">2</div>
    <div class="list" id="three">3</div>
    <div class="list" id="four">4</div>
</div>
<div class="link">
    <a class="click" href="#one">1</a>
    <a class="click" href="#two">2</a>
    <a class="click" href="#three">3</a>
    <a class="click" href="#four">4</a>
</div>

```

## CSS

```CSS
.box {
	width: 200px;
	height: 100px;
	border: 1px solid #ddd;
	overflow: hidden;
}

.list {
	width: 200px;
	height: 100px;
	line-height: 100px;
	background: #ddd;
	font-size: 80px;
	text-align: center;
}

.link {
	width: 200px;
	padding-top: 10px;
	text-align: right;
}

.click {
	display: inline-block;
	width: 20px;
	height: 20px;
	line-height: 20px;
	border: 1px solid #ccc;
	background: #f7f7f7;
	color: #333;
	font-size: 12px;
	font-weight: bold;
	text-align: center;
	text-decoration: none;
}

.click:hover {
	background: #eee;
	color: #345;
}

```

## 方法二
# 效果展示
[点击查看效果](https://hakunamatata052.github.io/blog/example/2.html)

# 实现原理
基于控件元素focus触发滚动重定位

# 缺点
选项卡内容切换的时候，还是“邦邦邦”这种干巴巴的效果，并没有滑来滑去那种湿湿的效果

# 具体代码
## HTML
```HTML
<div class="box">
    <div class="list"><input id="one">1</div>
    <div class="list"><input id="two">2</div>
    <div class="list"><input id="three">3</div>
    <div class="list"><input id="four">4</div>
</div>
<div class="link">
    <label class="click" for="one">1</label>
    <label class="click" for="two">2</label>
    <label class="click" for="three">3</label>
    <label class="click" for="four">4</label>
</div>

```

## CSS

```CSS
.box {
    width: 20em;
    height: 10em;
    border: 1px solid #ddd;
    overflow: hidden;
}
.list {
    height: 100%;
    background: #ddd;
    text-align: center;
    position: relative;
}
.list > input { 
  position: absolute; top:0; 
  height: 100%; width: 1px;
  border:0; padding: 0; margin: 0;
  clip: rect(0 0 0 0);
}

```
