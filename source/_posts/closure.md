---
title: 闭包
date: 2017-07-17 15:15:06
tags: js
---
## 闭包的含义
闭包是指有权利访问另一个函数作用域中的变量
### 最常见的闭包
1.循环里面的闭包
    for(var i = 0; i < 10; i++) {

        setTimeout(function() {
            console.log(i);
        }, 3000);

    }
运行结果是：10个10;
显然这不是我们想要的结果，如何解决
第一种方法：
<pre>
    function a(i) {
        setTimeout(function() {
            console.log(i);
        }, 1000);
    }
    for(var i = 0; i < 10; i++) {
        a(i)
    };
</pre>
第二种方法:
<pre>
    for(var i = 0; i < 10; i++) {
        (function(e) {
            setTimeout(function() {
                console.log(e);
            }, 3000);
        })(i);
    }
</pre>
第三种方法：
<pre>
    var i = 0;
    for(var j = 0;j < 10;j++) {
      setTimeout(function(){console.log(i);i++;},1000*j);
    }
</pre>
第四种方法：
<pre>
    for(let i = 0; i < 10; i++) {
       setTimeout(function() {
            console.log(i);
        }, 3000);
    }
</pre>
    let解析：将var改成了es6的let，一切问题都解决了。
    var存在闭包问题的原因是：es6之前，只有函数才有作用域的概念，其他无块级作用域这个概念，但是es6有了。
for循环结束后i=10,我们内部的函数是只能读取到 i = 10这个值的。因为保留在父级函数的活动对象中的i是父级函数执行完毕后i的值，也就是10。
所以方法二为了取到for循环中的每个i值，就需要再建立一个闭包函数，在第一层闭包中我们传入一个参数e，
在第二个闭包也就是第二层闭包中我们引用这个参数，而这个参数我们在自执行的时候把i传递进去，
也就是说，这个内部的闭包函数保留了第一层闭包函数活动对象中的e，而这个e是for在循环时所传递进来的每一个i的值。
let创建了块级作用域，并且执行完之后，i会被回收。
#### let的几个特性：
不存在变量提升问题;
不可以重复声明，包括和var一起声明;

方法一的解释和let一样，因为es5中函数是有自己的作用域的。


参考：https://johanzhu.github.io/2016/09/26/ten/
代码地址：https://github.com/zthappy/Javascript/blob/master/Closure/closure.html




