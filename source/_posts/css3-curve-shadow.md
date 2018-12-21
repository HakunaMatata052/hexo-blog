---
title: css3曲线投影
date: 2018-12-19 17:38:12
tags: [css,css3]
categories: "CSS"
---

### 模仿纸张曲线投影

# 效果展示
![效果图](https://image.zhangxinxu.com/image/blog/201012/2010-12-12_215403.png)
<!-- more -->


# 实现原理
首先，曲线投影的终效果其实是多投影重叠的效果：一点点倾斜的投影重叠一个直直的投影。
一般的直来直往的投影显然是使用box-shadow属性就可以搞定了。至于那个倾斜的投影，如果是现代浏览器，则需要就是CSS3变换属性transform（具体参见之前的“CSS3 Transitions, Transforms和Animation使用简介与应用展示”一文）。首先是倾斜，5度左右的样子，然后让其在主投影的后面显示就可以了。然后，单单只有倾斜是不够的，因为有一个脚会从一侧露出来，这很好理解。假设两个矩形一样大，位置完全重叠，如果发生旋转，则必定有边角不重合而露出来。即使矩形尺寸不一样，只要其以一个公共的边角旋转，至少会有两个角露出来，而实际上我们只需要一个，也就是斜边投影的哪个角。那么这个问题该如何解决呢，也很简单，同样是transform，不过这回不是旋转，而是拉伸(skew)，将规整的矩形拉伸成平行四边形，可避免旋转的时候多余的角露出来。

对于不支持CSS3的IE浏览器，按照上面的原理，理论上也是可以模拟出曲线投影效果的。因为IE下的投影效果可以使用投影滤镜（效果生硬不推荐）实现，或是模糊滤镜实现（推荐），至于旋转也有旋转滤镜。但是，就性能和成本而言，是否应该使用很值得商榷。

# 具体代码
## HTML
```HTML
<div class="img"></div>
<!-- 图片的宽高可以在CSS里更改 -->
```

## CSS

```CSS
.img {
    display: inline-block;
    *display: inline;
    width: 200px;
    height: 248px;
    margin: 20px;
    background-color: #fff;
    border: 1px solid #eee;
    -webkit-box-shadow: 0 1px 4px rgba(0, 0, 0, 0.27), 0 0 60px rgba(0, 0, 0, 0.06) inset;
    -moz-box-shadow: 0 1px 4px rgba(0, 0, 0, 0.27), 0 0 40px rgba(0, 0, 0, 0.06) inset; 
    box-shadow: 0 1px 4px rgba(0, 0, 0, 0.27), 0 0 40px rgba(0, 0, 0, 0.06) inset;
    position: relative;
    *zoom: 1;
}

.img:before {
    -webkit-transform: skew(-15deg) rotate(-6deg);
    -moz-transform: skew(-15deg) rotate(-6deg);
    transform: skew(-15deg) rotate(-6deg);
    left: 15px;
}
.img:after {
    -webkit-transform: skew(15deg) rotate(6deg);
    -moz-transform: skew(15deg) rotate(6deg);
    transform: skew(15deg) rotate(6deg);
    right: 15px;
}

.img:before, .img:after {
    width: 70%;
    height: 55%;
    content: ' ';
    
    -webkit-box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    -moz-box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3); 
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    
    position: absolute;
    bottom: 10px;
    z-index: -1;	
}
```

# 友情提示
这里的斜边投影使用的是负值z-index定位到本体阴影的后面的。由于使用的是z-index负值，所以，请务必保证当前投影元素的所有父标签均没有背景图片或背景色（body标签除外），否则，斜边投影是看不到的。

###### 原文链接
[CSS3 box-shadow实现纸张的曲线投影效果](https://www.zhangxinxu.com/wordpress/2010/12/css3-box-shadow%E5%AE%9E%E7%8E%B0%E7%BA%B8%E5%BC%A0%E7%9A%84%E6%9B%B2%E7%BA%BF%E6%8A%95%E5%BD%B1%E6%95%88%E6%9E%9C/)
