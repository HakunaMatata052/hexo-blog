---
title: 快速搭建webpack4.0+
date: 2020-08-25 14:14:00
tags: webpack
categories: 
    - JS
    - webpack
---
### 初始化npm
使用-y来快速创建
```
npm init -y
```
### 安装webpack和webpack-cli脚手架
从webpack4.0开始，webpack打包工具和命令行工具就开成两个包了，需要同时安装
```
npm i webpack webpack-cli -D
```
### 创建工程目录
新建src目录，之后写的js、html、css等源文件放在这里,在src目录下新建一个index.js作为入口文件
`src/index.js`是webpack默认的入口文件目录，因为不需要单独配置，如果不想使用这个路径，需要在`webpack.config.js`中单独配置
此处目录结构应为
- node_modules
- src
    - index.js
- package.json

### 安装webpack-dev-server
此时webpack只能每次执行打包命令后才能看到打包结果，开发过程中我们需要实时编译，因此需要一个本地服务
```
npm i webpack-dev-server -D
```
### 安装html-webpack-plugin插件
虽然现在可以试试打包js，但是我们的html依然不能进行热更新，而且打包上线时，打包的资源文件一般会进行哈希命名，每次打包手动修改index.html文件中的资源文件名着实很费劲
因此需要html-webpack-plugin插件帮我们自动完成资源引用并增加热更新功能
```
npm i html-webpack-plugin -D
```
安装好后在项目根目录下新建`webpack.config.js`文件，并设置html-webpack-plugin的对应html模板
```js
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports ={
    plugins:[
        new HtmlWebpackPlugin({
            filename:'index.html',
            template:"./src/index.html"
        })
    ]
}
```
在src下新建index.html文件
之后目录应为
- node_modules
- src
    - index.js
    - index.html
- package.json
- webpack.config.js

### 新增命令行
在`package.json`的scripts中新增一个命令
```js
...
"scripts": {
    "dev":"webpack-dev-server --host 192.168.0.2 --hot --https --port 80 --open",
    "test": "echo \"Error: no test specified\" && exit 1"
},
...
```
其中
`--host 192.138.0.2`表示配置本地服务的ip
`--hot`表示开启热更新模式
`--https`表示开始https
`--port 80`表示端口为80
`--open`表示启动后自动打开游览器，后面可以跟游览器的标识，不写表示打开默认游览器
到此本地服务就搭建完毕了，接下来需要配置loader和打包选项，今天先更到这里





