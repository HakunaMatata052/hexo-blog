---
title: 制作菱形图片遮罩
date: 2019-03-01 10:56:52
tags: CSS CSS3
categories: CSS
---
# 方法一
使用box-shadow制作菱形遮罩

需要在原有结构内增加一个shaow遮罩层

### HTML
```html
    <div class="img">
        <img src="https://picsum.photos/300/300">
        <div class="shadow"></div>
    </div>
```
<!--more-->
外层div设置相对定位position: relative;
将shadow层旋转45度，并设置阴影；
box-shadow中的值分别是：
box-shadow：水平位移 垂直位移 阴影宽度 模糊程度 颜色
这里水平和垂直位移这只为0，即从中间开始向四周出现阴影。 阴影宽度一定要宽于外框，模糊程度可以填0，即不模糊，颜色填白色。
### CSS
```css
        .img {
            width: 300px;
            height: 300px;
            position: relative;
            margin: 100px auto;
            overflow: hidden;
        }

        .shadow {
            width: 200px;
            height: 200px;
            box-shadow: 0px 0px 0px 200px #fff;
            transform: rotate(45deg);
            position: absolute;
            left: 50%;
            top: 50%;
            margin-left: -100px;
            margin-top: -100px;
            border-radius: 10px;
        }
```
### 效果
<iframe src="{% asset_path mark.html %}" width="600" height="600" frameborder="no" border="0" marginwidth="0" marginheight="0" allowtransparency="yes"></iframe>

# 方法二
使用两次旋转达到菱形效果
### HTML
```html
<div class="img">
    <img src="https://picsum.photos/300/300">
</div>
```
### CSS
```css
.img {
    position: relative;
    width:200px;
    height: 200px;
    margin: 50px auto;
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -o-transform: rotate(45deg);
    transform: rotate(45deg);
    border-radius: 10px;
    overflow: hidden;
}
.img img {
    position: absolute;
    left: 50%;
    top: 50%;
    display: block;
    width: 500px;
    height: 500px;
    margin-top: -250px;
    margin-left: -250px;
    -webkit-transform: rotate(-45deg);
    -moz-transform: rotate(-45deg);
    -o-transform: rotate(-45deg);
    transform: rotate(-45deg);
}
```


### 效果
<iframe src="{% asset_path mark2.html %}" width="650" height="500" frameborder="no" border="0" marginwidth="0" marginheight="0" allowtransparency="yes"></iframe>
