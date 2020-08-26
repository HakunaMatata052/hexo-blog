---
title: Vuex的使用
date: 2018-12-19 16:25:36
tags: 
	- vue
	- vuex
categories: ["JS","VUE"]
---

![VUEX](/images/01.jpg)
<!-- more -->

## Vuex的使用
### 安装Vuex

```npm
npm install vuex --save
```
> 淘宝镜像
```npm
cnpm install vuex --save
```
### 新建js文件
可以放在store文件夹中命名为index.js



```javascript
import Vue from 'vue'
import vuex from 'vuex'
Vue.use(vuex);

export default new vuex.Store({
	state: {
		api:'http://wjdh03.sjgogo.cn/api/',
		token:"57373A7E05CB44079B2F12C14A5E83A9",
		domain: "http://www.baidu.com",
		notice: true,
	},
	mutations: {
		domainURI(url) {
			var durl = /http:\/\/([^\/]+)\//i;
			var domain = url.match(durl);
			return domain[1];
		}
	}
})
```
### 调用Vuex
main.js中引入Vuex并使用

```javascript
import store from './store'  //引入Vuex
```
载入Vuex
```javascript
const vue = new Vue({
  router,
  store,   //载入Vuex
  render: h => h(App)
}).$mount('#app')
```
### 使用全局状态（变量）
在需要使用的组件中 使用{{$store.state.domain}}调用


