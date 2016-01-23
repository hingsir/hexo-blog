title: 检测jquery对象是否存在
date: 2016-01-23 12:02:34
tags:
 - JavaScript
categories:
 - 技术杂谈
---
检测jquery对象是否存在
>2016-01-21 by [@hingsir](https://github.com/hingsir)

检测`$(selector)`是否存在，相信不少人写过类似下面的代码：
```js
if($(selector)){
    // do something
}else{
    //do other things
}
```
然而这样写是有问题的，因为`$(selector`返回的是一个object，即便未匹配到任何元素，也会返回空数组`[]`。`ToBoolean([])`为true，那么else代码块永远也不会执行到，因此我们一般利用`$(selector).length>0`来检测。