---
title: :before :after
date: 2017-09-15 14:56:32
tags: css
---
### 自从我学会了用before 和after伪元素
便一发不可收拾，写啥css之前都要想想能不能用before和after来实现


## before，after

before所有主流浏览器都支持
表示在元素之前，例如
<pre>
&lt;div class="test1"&gt;你好&lt;/div&gt;
.test1:before {
    content:"hello"
}
</pre>

结果为： hello你好
同理after
after表示在元素后面添加content


## 单冒号 与 双冒号 的区别

一个冒号代表 伪类，如：:hover :active :link :visited :focus :first-child :lang


另一种解释是： 伪类用于向某些选择器添加特殊的效果

两个冒号代表 伪元素，如： before after first-line first-letter


另一种解释是：伪元素用于将特殊的效果添加到某些选择器


中文的含义真的是博大精深，反正我没懂上面的那个解释


所以大概的解决办法是：就用单冒号



### 使用before和after的好处
#### 1.最近一直在写小程序，对于dom节点的要求是越精简越好，不然一直会遇到dom节点超大的报错，很是纠结，此时此刻，before和after华丽登场
做个比较吧

![tuian](http://op3y7nhgg.bkt.clouddn.com/choose1.png)



在之前的写法是


<pre>
.btn {
    border:1px solid #23beae;
    height: 30px;
    width: 110px;
    line-height: 28px;
    font-size: 12px;
    border-radius: 5px;
    text-align: center;
    position: relative;
}
.btn img {
    position: absolute;
    bottom: 0;
    right: 0;
}
&lt;div class="btn"&gt;Test&lt;img src="http://op3y7nhgg.bkt.clouddn.com/choose.png"&gt;&lt;/div&gt;
</pre>

还是需要两个节点的

现在的写法是：



<pre>
    .fromCityListact {
        color:#23beae;
        border:1px solid #23beae;
        width: 110px;
        height: 30px;
        line-height: 30px;
        text-align:center;
        position: relative;
    }
    .fromCityListact:after {
        content: "";
        position: absolute;
        bottom: 2px;
        right: 3px;
        width: 3px;
        height: 6px;
        border-right: 1px solid #fff;
        border-bottom: 1px solid #fff;
        transform:rotate(45deg);
    }
    .fromCityListact:before {
        content: "";
        position: absolute;
        bottom: 0;
        right: 0;
        width: 0;
        height: 0;
        border-bottom: 15px solid #23beae;
        border-left: 15px solid transparent;
    }
    &lt;div class="fromCityListact"&gt;Test2&lt;/div&gt;
</pre>


  虽然只是少了一个节点，但是我的菜单是循环的，一百条就少了一百个节点。



  慢慢的爱上了 before


#### 2.  0.5px 的线



<pre>
.thin-border-top {
    position: relative;
}
.thin-border-top:before{
    content: '';
    position: absolute;
    width: 200%;
    height: 1px;
    top: 0;
    border-bottom: 1px solid #000;
    transform-origin: 0 0;
    transform: scale(.5,.5);
    box-sizing: border-box
}
&lt;div class="thin-border-top"&gt;&lt;/div&gt;
</pre>

#### 3.反正能少写一个节点是是一个
