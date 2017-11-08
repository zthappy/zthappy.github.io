---
title: js忽略的一些细节
date: 2017-07-24 16:32:23
tags: js
---
## 1.A.style.left

html如此

<pre>
    &lt;div class="smallkedu" id="move"$gt;1 2 3 4 5 6 7 8 9 1 2 3 4 5 6 7 8 9 1 2 3 4 5 6 7 8 9&lt;/div&gt;
</pre>
css如此
<pre>
    #move {
		background-color: #fff;
		height: 40px;
		width: 2080px;
		position: absolute;
		bottom:5px;
		left:0;
	}
</pre>
毫无毛病，我现在想要在js种获取css的某个值，js如此
<pre>
    var movediv = document.getElementById("move");
    var x = movediv.style.left;
    console.log(x);
</pre>
也毫无毛病，但是控制台就是打印不出left值；
我设置 movediv.style.backgroundColor = #fff
实现了颜色变化，所以说明我的语法没有问题。
上网搜索了很久，终于找到答案：
 A.style.left 只针对行内样式;
 所以将 html改成以下方式即可
 <pre>
    &lt;div class="smallkedu" id="move" style="left:0"&gt;1 2 3 4 5 6 7 8 9 1 2 3 4 5 6 7 8 9 1 2 3 4 5 6 7 8 9&lt;/div&gt;
 </pre>