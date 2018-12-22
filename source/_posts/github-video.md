---
title: 利用Github上传并引用video资源
date: 2018-12-21 15:56:58
tags: github
categories:
---

> 很多网站都有背景视频的元素，利用的是【HTML5】的新特性————【video】标签
例如：[点击打开](http://www.hearttrip.net/tourlist.html) 里面的banner背景，就是一个视频

<!-- more -->

具体代码：
```html
<video src="video.mp4" controls="controls">
您的浏览器不支持 video 标签。
</video>
```
但是对于很多服务器来说，视频太站资源，太耗流量，但是将视频上传到优酷、腾讯视频上又无法获得视频真实地址（video标签中的视频必须是视频的物理地址，即必须以.mp4等的拓展名结束的地址），而且还有广告
这里推荐一个简单的方法：

》 使用GitHub等git托管网站上传视频

## 方法

### 注册
首先注册一个GitHub账号 [点我注册](https://github.com/)
{% asset_img 01.jpg %}

### 新建项目
点击New新建一个项目，名称可以随便取，但是不能写中文,填写好后点击【Create repository】
> 需要注意的是 必须选中Initialize this repository with a README这个选项，否则你需要安装git使用指令将视频传上去。

{% asset_img 02.jpg %}
{% asset_img 03.jpg %}

### 上传视频
新建号项目你将看到这样的界面，点击【Upload files】上传你的视频就可以，最后上传完了之后点击【Commit changes】
{% asset_img 04.jpg %}
{% asset_img 05.jpg %}

### 引用视频
上传完毕后就能在项目中看到你的视频，点击视频后再复制【View Raw】的连接就可以获得视频的真实地址了，例如我的连接是：https://github.com/HakunaMatata052/video/blob/master/a.mp4?raw=true
注意：视频最后的 ?raw=true 不能删除，否则视频无法播放
{% asset_img 06.jpg %}

最后放在代码里看一下
```html
<video src="https://github.com/HakunaMatata052/video/blob/master/a.mp4?raw=true" controls="controls">
您的浏览器不支持 video 标签。
</video>
```

效果：
<video src="https://github.com/HakunaMatata052/video/blob/master/a.mp4?raw=true" controls="controls" autoplay="autoplay">
您的浏览器不支持 video 标签。
</video>

> 如果想让视频当背景用的话，需要设video为自动播放，可以设置autoplay="autoplay"具体代码如下

```html
<video src="https://github.com/HakunaMatata052/video/blob/master/a.mp4?raw=true" controls="controls"  autoplay="autoplay">
您的浏览器不支持 video 标签。
</video>
```

如果需要隐藏播放控件可以去掉 controls="controls" ，也可以使用css
```css
video::-webkit-media-controls {
  display:none !important;
}
```