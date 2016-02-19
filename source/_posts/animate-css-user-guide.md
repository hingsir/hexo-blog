title: Animate.css 使用指南
date: 2016-02-19 16:51:28
tags:
 - CSS
 - NodeJs
categories:
 - 技术杂谈
---

[hingsir.com](http://hingsir.com/)首页的动画效果使用的是第三方动画库[Animate.css](https://github.com/daneden/animate.css)，它包含了很多酷炫的动画效果（[点击这里查看](https://daneden.github.io/animate.css/)），基本的使用方法如下：

* 引入css文件
```html
<head>
  <link rel="stylesheet" href="animate.min.css">
</head>
```
* 给需要动画效果的元素添加对应的class
```html
<div class="animated fadeIn">fadeIn</div>
```
* 自定义动画的显示时机和持续时间
```css
#yourElement {
  -vendor-animation-duration: 3s;
  -vendor-animation-delay: 2s;
  -vendor-animation-iteration-count: infinite;
}
```

是不是非常简单！但是尽管进行了压缩，`animate.min.css`仍然有50kb那么大，那么有办法再进一步精简吗？就比如我只用到了`bounce` `bounceInDown` `zoomIn`，完全没必要引入所有动画效果。接下来将教你如何定制自己的动画库

* 克隆animate.css库到本地
```bash
$ git clone https://github.com/daneden/animate.css.git
```
* 安装npm依赖
```bash
$ npm install
```
* 修改`animate-config.json`（建议先备份）
将不需要的动画效果全删掉，最后留下
```json
{
  "attention_seekers": [
    "bounce"
  ],
  "bouncing_entrances": [
    "bounceInDown"
  ],
  "zooming_entrances": [
    "zoomIn"
  ]
}
```
* 生成animate.min.css
```base
$ gulp
```
animate.min.css只剩下4kb，大功告成！