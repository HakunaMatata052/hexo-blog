---
title: Vue全局公用函数
date: 2018-12-21 11:00:29
tags: vue
categories: 
    - js
    - vue
---

> 经常在做项目的时候会遇到一个函数在很多组件和页面中调用，如计算时间差，刷新token等操作，这时就需要定义一个全局都能调用的函数

<!-- more -->


## 新建js文件
可以放在src的utils文件中，命名index.js


```javascript
exports.install = function (Vue, options) {
    Vue.prototype.changeData = function (){
        alert('执行成功');
    };
};
```
## 调用函数
在需要调用函数的组件内引入Vue和该函数文件

```javascript
import Vue from 'vue'               //引入Vue
import base from '../../utils'      //引入新建的公用函数js
Vue.use(base);                      //使用新建的公用函数js
```
> 如果需要全局引用，则将调用函数写在main.js中即可