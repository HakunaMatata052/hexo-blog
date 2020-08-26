---
title: Promise和async/await
date: 2020-08-25 11:18:00
tags: Promise async/await async await 同步异步 异步
categories: 'JS'
top: true
---
### 为什么要用Promise
一般情况我们一次性调用API就可以完成请求。
有些情况需要多次调用服务器API，就会形成一个链式调用，比如为了完成一个功能，我们需要调用API1、API2、API3，依次按照顺序进行调用，这个时候就会出现回调地狱的问题

### Promise的链式结构
使用Promise可以做到链式结构，即一个请求结束后在then方法中执行下一个异步请求，再下一个异步请求放在上一个异步请求的then方法中,但是需要再每个then方法中return一个Promise对象
这样我们就得到了一个扁平的结构而不是回调套回调。
eg.
```js
new Promise((res, rej) => {
    setTimeout(() => {
        console.log(1)
        res()
    }, 1000);
}).then(() => {
    return new Promise((res2, rej2) => {
        setTimeout(() => {
            console.log(2)
            res2()
        }, 1000);
    })
}).then(() => {
    return new Promise((res3, rej4) => {
        setTimeout(() => {
            console.log(3)
            res3()
        }, 1000);
    })
}).then(() => {
    console.log('结束')
})
```
<!--more-->
执行结果是
```js
1
2
3
结束
```
### 使用all方法
但是通常在真是项目中，每个请求会有单独的方法封装，而且每个Promise会有独立的then方法，这时可以使用Promise对象的all方法
他表示无论三个异步请求谁先执行谁后执行，都等待三个异步请求全部结束后执行all中的函数。
如果后一个请求需要得到前一个请求中的数据，那么还是需要使用前面的链式结构才行。
如果既要使用已经封装好的Promise函数，有需要按步调用，可以使用ES7中的async/await
eg.
```js
const promise1 = new Promise((res, rej)=>{
    setTimeout(() => {
        console.log(1)
        res()
    }, 1000);
})
const promise2 = new Promise((res, rej)=>{
    setTimeout(() => {
        console.log(2)
        res()
    }, 3000);
})
const promise3 = new Promise((res, rej)=>{
    setTimeout(() => {
        console.log(3)
        res()
    }, 2000);
})
Promise.all([promise1, promise2, promise3]).then(()=> {
  console.log('结束');
});
```
执行结果是
```js
1
3
2
结束
```
### async/await
首先封装的方法需要return一个Promise对象，接着在请求的函数前面添加async关键字，在请求函数的内部使用变量或常量接受封装的Promise对象即可，但是封装的Promise对象前需要加await
这时接收到的结果就是Promise对象中then方法中return的结果
```js
function ajax(){
    return new Promise((resolve, reject)=>{
        setTimeout(() => {
            resolve("666")
        }, 5000);
    }).then(res=>{
        return res
    })
}
async function ajaxAsync(){
    console.log(1)
    const r = await ajax()    
    console.log(2)
    console.log(r)    
    console.log(3)
}
ajaxAsync()
```
执行结果是
```js
1
2  // 5s后
666
3
```