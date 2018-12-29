---
title: 无JS实现在线客服的切换效果
date: 2018-12-20 15:05:17
tags:
    - css
    - css3
categories: CSS
top: true
---

首先可以看下效果
[点我查看](http://www.lofly.cn/)

这里利用HTML的 【checkbox】类型的【input】和【label】元素的【for】属性
和CSS的【:checked】选择器以及【~】选择器

主要的原理是点击【label】使【label】的【for】属性指定id【input】改变选中状态（【:checked】），
【input】选中状态改变后，使用css改变【input】后面的元素的显示或隐藏（或定位）。

<!-- more -->

# 首先你必须知道<label>元素的for属性可以控制【checkbox】类型的【input】
> 例如：

```html
<input type="checkbox" id="dome">

<label for="dome">切换</label>
```
> 效果:
<iframe src="{% asset_path 01.html %}" width="600" height="100" frameborder="no" border="0" marginwidth="0" marginheight="0" allowtransparency="yes"></iframe>

# 然后利用CSS的 ~ 选择器 设置input被选中后紧跟的元素的样式
> 多提一句
> ~ 选择器表示元素后的同胞元素
如：
```CSS
p~ul{
　　background:#ff0000;
}
```
```HTML
<p>快乐生活</p>
<ul>
　　<li>生活</li>
　　<li>生活</li>
　　<li>生活</li>
</ul>
```
会给p元素后所有的ul元素加背景

那么我们需要做的就是为input后的元素做隐藏显示（或改变定位）
如何判断需要显示还是隐藏呢？
需要用到input的checked属性

> 如果需要改变默认状态可以给input加checked="checked"

# 最后具体代码如下

## HTML
```html
<div class="dome">
    <input type="checkbox" id="toggle">
    <div class="open">
        <label for="toggle">关闭</label>
        打开以后你看到的
    </div>
    <div class="close">
        <label for="toggle">打开</label>
        关闭以后你看到的
    </div>
</div>
```

## CSS
```css
#toggle {
    display:none;
}
#toggle~.open {
    display:block;
}

#toggle~.close {
    display:none;
}

#toggle:checked~.open {
    display:none;
}

#toggle:checked~.close {
    display:block;
}
```

> 效果：

<iframe src="{% asset_path 02.html %}" width="600" height="500" frameborder="no" border="0" marginwidth="0" marginheight="0" allowtransparency="yes"></iframe>
