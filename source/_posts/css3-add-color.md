---
title: PNG格式小图标的CSS任意颜色赋色技术
date: 2018-12-19 17:50:12
tags: css3
categories: "CSS"
---

### PNG格式小图标的CSS任意颜色赋色技术

`**注意**：PC某些浏览器不支持，请勿使用，手机端可以使用`

<!-- more -->
# 主要代码
```css
filter: drop-shadow(rgb(62, 243, 52) 20px 0px);
```
# 实现原理
原理其实很简单，使用了CSS3滤镜filter中的drop-shadow，drop-shadow滤镜可以给元素或图片非透明区域添加投影。

如果对drop-shadow不是很了解，建议先看看前些时间写的“CSS3 filter:drop-shadow滤镜与box-shadow区别应用”一文！

对于背景透明的png小图标而言，如果我们施加一个不带模糊的投影，不就等同于生成了另外一个颜色的小图标了吗？

然后，我们把原始图标隐藏在容器外面，投影图标在容器中间，不见给人感觉是赋色效果了？

比方说本文的demo，如果把icon父级的的 *overflow:hidden* 去掉，原始的图标就暴露出来啦！

![效果图](https://image.zhangxinxu.com/image/blog/201606/2016-06-08_004748.png)

# 具体代码

## HTML
```html
<i class="icon">
	<i class="icon icon-del"></i>
</i>
```

```css
 .icon { /*图标元素必须是块级元素，有宽高，切必须溢出隐藏*/
    display: inline-block;  
    width: 20px;
    height: 20px;
    overflow: hidden;
}
.icon > .icon {
    position: relative;
    left: -20px; /*-20px为图标宽度，必须是负值*/
    border-right: 20px solid transparent;
    -webkit-filter: drop-shadow(rgb(62, 243, 52) 20px 0px); /*20px为图标宽度*/
    filter: drop-shadow(rgb(62, 243, 52) 20px 0px);  /*20px为图标宽度*/
    background: url(delete.png) no-repeat center;   /*图标png文件设置在包裹内的div中切必须是块级元素，有宽高*/
}
```

## 兼容性
IE13+支持，Chrome和FireFox浏览器支持，移动端iOS支持，Android4.4+支持。也就是，基本上，移动端现在可以使用这种技术了。
既节约了流量，也让我们的开发更简单，维护更方便了。