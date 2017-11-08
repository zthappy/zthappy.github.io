---
title: css水平居中和垂直居中
date: 2017-07-27 13:58:29
tags: css
---
## 水平居中
1.文字的水平居中
<pre>text-align:center;</pre>
但是也不是所有情况都能够适用的，只有在元素标签具有宽度的时候才起效。
元素的display具有以下四种状态：inline，block,inline-block,none
inline 是不能设定宽度的，none是整个元素消失。
所以文字的水平居中的前提是将元素的display设置成inline-block,或者是block
    <div class="word">block文字居中</div>
	<label class="word2">inline文字居中</label>
	<span class="word3">inline-block文字居中</span>
block文字居中完全没有问题，inline文字居中需要先设置display和width，inline-block需要设置width；
但是inline-block会产生空隙。
2.元素居中(父元素宽度已知，子元素为块级元素)
    <pre>margin:0 auto;</pre>
    例子：
    html
    <pre>
        &lt;div class="sym"&gt;
            &lt;div class="sym1"&gt;abc&lt;/div&gt;
        &lt;/div&gt;
    </pre>
    css:
    <pre>
        .sym {
                text-align: center;
        }
        .sym1 {
            height: 100px;
            width: 100px;
            background-color: pink;
            margin: 0 auto;
        }
    </pre>
    前提条件，已知宽度。宽度设置同上。
3.元素居中(父元素宽度已知，子元素为行内元素或者inline-block)
<pre>text-align:center;</pre>
例子：
    html
    <pre>
        &lt;div class="sym2"&gt;
            &lt;div class="sym3"&gt;abc&lt;/div&gt;
        &lt;/div&gt;
    </pre>
    css:
    <pre>
        .sym2 {
            text-align: center;
        }
        .sym3 {
            display: inline-block; // inline
            border:1px solid #999;
        }
    </pre>
4.transform标签和绝对定位联合使用
例子：
    html
    <pre>
        &lt;div class="par1"&gt;
            &lt;div class="son1"&gt;abc&lt;/div&gt;
        &lt;/div&gt;
    </pre>
    css:
    <pre>
        .son1 {
        		position:absolute;
        	  	left:50%;
        	  	transform:translate(-50%,0);
        	  	border:1px solid pink;
        	}
    </pre>
5.绝对定位和负值margin-left联合使用
例子：
    html
    <pre>
        &lt;div class="par2"&gt;
            &lt;div class="son2"&gt;abc&lt;/div&gt;
        &lt;/div&gt;
    </pre>
    css:
    <pre>
        .son2 {
        		position: absolute;
                width: 100px;
                left: 50%;
                margin-left:-50px;
        	}
    </pre>

## 垂直居中
1.单行文本垂直居中 line-height
line-height 和 height 保持一致
<pre>
    <div class="ver1">
		文字垂直居中
	</div>
	.ver1 {
        height: 100px;
        line-height: 100px;
        background-color: pink;
    }
</pre>

2.vertical-align 垂直居中
vertical-align 的定义：
该属性定义&lt;行内元素&gt;的基线相对于该元素所在行的基线的垂直对齐。
需要有参考值标签
参考：https://segmentfault.com/a/1190000002668492

3.margin-top:已知两者高度

4.定位

5.table中的水平居中和垂直居中可以较好的使用text-align 和 vertical-align

