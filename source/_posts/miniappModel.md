---
title: miniappModel
date: 2017-11-08 14:28:55
tags: 小程序
---

## 小程序api自带弹框
wx.showModal(title,content,showCancel,cancelText,cancelColor,confirmText,confirmColor,success,fail,complete)


自带的弹框已经很完美的，唯一美中不足的是，我们能改的只有文本的颜色，不能修改
所以我们在设计妹子的催促下，开始了自定义弹框组件的开发。

## 小程序模板
# 定义模板
<pre>
    <template name="msgItem">
      <view>
        <text> {{index}}: {{msg}} </text>
        <text> Time: {{time}} </text>
      </view>
    </template>
</pre>

# 使用模板
<pre>
    <template is="msgItem" data="{{...item}}"/>
</pre>

模板的使用可以让页面部分共用，但是不好的一点是，js需要在每个引用的页面中重新定义，并没有很好的起到复用代码的作用。
