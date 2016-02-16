title: 浏览器后退页面不刷新的问题
date: 2016-02-16 16:54:55
tags:
 - Web
categories:
 - 技术杂谈
---

做项目的过程中遇到这样一个问题：提交表单到下一页，再点击浏览器后退按钮回到表单页，发现部分表单数据丢失或者还是旧的数据。检查响应头，确实设置了`Cache-control:no-cache`，但浏览器还是偷懒`from cache`了。百度，google了一圈发现解决方案都不尽如意，最后在SOF里输入几个英文关键字找到下面的问答完美解决。

[Force reload/refresh when pressing the back button](http://stackoverflow.com/questions/9071838/force-reload-refresh-when-pressing-the-back-button?lq=1)

仅仅设置`Cache-control:no-cache`并不够，还需设置`Expires` `Last-Modified` `Pragma`

PHP实现
```php
// any valid date in the past
header("Expires: Mon, 26 Jul 1997 05:00:00 GMT");
// always modified right now
header("Last-Modified: " . gmdate("D, d M Y H:i:s") . " GMT");
// HTTP/1.1
header("Cache-Control: private, no-store, max-age=0, no-cache, must-revalidate, post-check=0, pre-check=0");
// HTTP/1.0
header("Pragma: no-cache");
```
其他语言可参照着进行相应的设置。