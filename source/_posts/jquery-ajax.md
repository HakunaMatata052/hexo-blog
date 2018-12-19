---
title: jQueryAjax请求完全版
date: 2018-12-19 17:34:07
tags: [js,jquery]
categories: ["JS","jQuery"]
---

### jQueryAjax请求完全版

```javascript
$.ajax({
    async: true, //true异步，false同步
    url: '/uploads/rs/419/nvhogkww/data.json',
    type: 'get',
    complete: function(XHR, TS) { alert('complete'); }, //完成回调函数(XHR, TS)
    error: function(XMLHttpRequest, textStatus, errorThrown) {
        //XMLHttpRequest.readyState:
        //0 － （未初始化）还没有调用send()方法
        //1 － （载入）已调用send()方法，正在发送请求
        //2 － （载入完成）send()方法执行完成，已经接收到全部响应内容
        //3 － （交互）正在解析响应内容
        //4 － （完成）响应内容解析完成，可以在客户端调用了
        //XMLHttpRequest.status:
        //textStatus: "timeout", "error", "notmodified" 和 "parsererror"。
        //（0）null
        //（1）timeout 超时
        //（2）error
        //（3）notmodified 未修改
        //（4）parsererror 解析错误
        console.log('错误1：' + XMLHttpRequest.readyState);
        console.log('错误2：' + textStatus);
        console.log('错误3：' + errorThrown);
    }, //默认值: 自动判断 (xml 或 html)。请求失败时调用此函数。有以下三个参数：XMLHttpRequest 对象、错误信息、（可选）捕获的异常对象。
    success: function(response) { alert('success'); }
});
```