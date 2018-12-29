---
title: Hexo添加置顶功能和标识
date: 2018-12-29 17:29:09
tags: 
    - Hexo
    - next
categories: hexo
---

首先看下效果
![效果图](https://i.loli.net/2018/12/29/5c273ed38214d.png)
<!--more-->
## 具体实现
### 安装插件
```
$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
```
### 新建/修改 文章
新建或修改文章时在文章**Front-matter**中加入**top: true**即可
```
---
title: 无JS实现在线客服的切换效果
date: 2018-12-20 15:05:17
tags:
    - css
    - css3
categories: CSS
top: true
---
```
> 到此为止，文章的置顶功能就实现了,但是我们还需要给置顶的文章加个标识，如
![](https://i.loli.net/2018/12/29/5c2740bd13582.png)
So，我们需要加一个图标或者文字标签
这里我做了一个简单的，你可以修改一下，做一个好看的图标
### 添加标识
如果你使用的是**next**的主题，打开目录**themes/next/layout/_macro**，找到文件post.swig，搜索
```
</{% if theme.seo %}h2{% else %}h1{% endif %}>
```
大概在65行，在他上面添加
```
{% if post.top %}
    <span style="color:#f00;border:1px solid #f00;padding:2px 5px;font-size:12px;">置顶</span>
{% endif %}
```
这是你会发现标识出现了，但是高度有些错位，在**themes/next/source/_custom**中找到**custom.styl**文件，添加一行
```css
.posts-expand .post-title {
  line-height:1
}
```
这时你就可以看到具体的效果了
> 当然你可以添加更好看的图标，只需要修改HTML和CSS即可。