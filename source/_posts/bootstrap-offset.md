---
title: 一句代码解决bootstrap栅格几个设置5等分
date: 2019-01-04 15:45:01
tags: 
    - bootstrap
    - offset
categories: 
    - HTML
    - BOOTSTRAP
---
HTML
```html
<div class="container">
    <div class="row">
        <li class="col-xs-offset-1 col-xs-2 text-center">苹果</li>
        <li class="col-xs-2 text-center">香蕉</li>
        <li class="col-xs-2 text-center">番茄</li>
        <li class="col-xs-2 text-center">石榴</li>
        <li class="col-xs-2 text-center">芒果</li>
    </div>
</div>
```
正常设置每个栅格2等分，最后会在末尾空余出2等分（共12等分），然后第一个栅格设置col-xs-offset-1，意思是偏移一格，等于把最后的2等分其中一份放在最前面了。
这样做可以解决bootstrap栅格5等分的问题，但是最终宽度会比正常窄，可以单独设置container的宽来解决。
