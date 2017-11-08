---
title: 关于viewport
date: 2017-07-25 15:22:07
tags: html
---
### 什么是viewport
viewport 是用户网页的可视区域。
### viewport meta 标签
<pre>&lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;</pre>
width：控制 viewport 的大小，可以指定的一个值，如果 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
height：和 width 相对应，指定高度。
initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
maximum-scale：允许用户缩放到的最大比例。
minimum-scale：允许用户缩放到的最小比例。
user-scalable：用户是否可以手动缩放。
### 使用viewport适配屏幕
移动端适配的方法：
1.高度固定，宽度自适应
2.宽度固定，使用viewport缩放
3.宽度rem，viewport缩放

#### 高度固定，宽度自适应
<pre>&lt;meta name="viewport" content="width=device-width,initial-scale=1"&gt;</pre>
如此设置之后，高度固定，宽度用百分比、定值或者flex都可以。

#### 宽度固定，使用viewport缩放
<pre>&lt;meta name="viewport" content="width=640,initial-scale=0.5,maximum-scale=0.5,minimum-scale=0.5,user-scalable=no"&gt;</pre>
width=640可以换成任意数值，viewport会根据不同屏幕缩放

#### 宽度rem，viewport缩放
根据屏幕宽度设定 rem 值，需要适配的元素都使用 rem 为单位，不需要适配的元素还是使用 px 为单位。