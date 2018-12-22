---
title: 利用iconfont.cn快速制作前端图标
date: 2018-12-22 10:28:36
tags:
categories:
---

> 以前不会用iconfont.cn的时候，只知道这是个图标库，可以吧图片下载下来，然后制作成图片，在写入HTML。
> 其实没有这么麻烦，iconfont支持三种图片引入方式——Unicode，字体，svg

<!-- more -->

## 注册账号
首先登录[iconfont](https://iconfont.cn) 这里我使用的是Github账号直接登录，你可以使用微博账号登录
{% asset_img 01.jpg %}

## 搜索图标
然后再首页搜索你需要的图标，可以使用中文搜索（建议英文）
{% asset_img 02.jpg %}

找到想要的图标之后不要点击下载按钮，要点击购物车按钮，这样才能将多个图片集合到一个项目里
{% asset_img 03.jpg %}

通常一个项目或网站肯定不止一个图，这时你可以继续搜素其他图标并加入购物车
当你需要将所有图标制作成网站需要的字体文件或者svg文件引入时，点击右上角的购物车按钮
{% asset_img 04.jpg %}

这里的三个选项分别是：
{% asset_img 05.jpg %}

| 名称| 解释| 
| ------------- |:------------------:|
| 添加至项目| 添加到新建或已有的项目（后期可继续添加图标）|  
| 下载素材| 下载购物车里的图标素材，最后可以下载AI，SVG,PNG格式的图片文件| 
| 下载代码| 下载生成的引入文件 包含CSS，font，svg等，与添加项目类似，但是后期无法继续添加图标| 

这里为了后期能够继续增加或删除图标，我们尽量选择添加至项目，如果没有项目，他会提示你新建项目，根据提示操作就好，这里不再赘述。

## 引用图标
制作好的图标可以在我的项目中看到,可以选择引用iconfont的远程地址（CDN方式），也可以下载到本地引入，如果是使用CDN方式，需要依次点击查看在线链接--生成链接
{% asset_img 06.jpg %}

### Unicode方式
需要在你的css中加入上面的代码
```css
@font-face {
  font-family: 'iconfont';  /* project id 978636 */
  src: url('//at.alicdn.com/t/font_978636_9jco6oz9c8i.eot');
  src: url('//at.alicdn.com/t/font_978636_9jco6oz9c8i.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_978636_9jco6oz9c8i.woff') format('woff'),
  url('//at.alicdn.com/t/font_978636_9jco6oz9c8i.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_978636_9jco6oz9c8i.svg#iconfont') format('svg');
}
```
如果某个地方需要使用图标，HTML和CSS分别是这样
#### HTML
```html
<div class="dome">
    &#xe654;
</div>
```
#### css
```css
.dome{
    font-family: 'iconfont';
}
```
这里的& # x e 6 5 4;就是图标对应代码
{% asset_img 07.jpg %}

### Font class
font class是一个链接，需要用link引入
#### html
```html
<link rel="stylesheet" href="//at.alicdn.com/t/font_978636_9jco6oz9c8i.css">
<div class="dome"></div>
```
#### css
```css
.dome{
    font-family: 'iconfont';
}
```

### symbol引用
拷贝项目下面生成的symbol代码：
#### HTML
```
//at.alicdn.com/t/font_8d5l8fzk5b87iudi.js
```
加入通用css代码：
#### css
```css
.icon {
       width: 1em; height: 1em;
       vertical-align: -0.15em;
       fill: currentColor;
       overflow: hidden;
    }
```
挑选相应图标并获取类名，应用于页面
#### html
```html
<svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-xxx"></use>
</svg>
```
这里的#icon-XXX对应图标代码 如icon-menu

> 最后，墙裂建议使用Font class方式引入，兼容度最高，图标大小可以通过font-size控制，颜色可以通过color控制，很方便。
