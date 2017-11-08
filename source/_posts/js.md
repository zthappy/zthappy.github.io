---
title: Js 数组循环比较
date: 2017-07-12 16:49:33
tags: js
---
### for循环
最简单最通用的循环，代码如下：
    for(var i = 0; i < arr.length;i++) {
        // 代码
    }
### 优化的for循环，代码如下：
    for(var i = 0, len = arr.length;i<len;i++) {
        // 代码
    }
### for..in 循环
    for(var i in arr) {
        // 代码
    }
### forEach循环，ie中无该方法，代码如下：
    arr.forEach(function(value,index,arr){
        // 代码
    })
### map 循环
    arr.map(function(value,index,arr) {
        // 代码
    })
### for..of循环 es6
    for(var i of arr) {
        // 代码
    }
## 测试代码：
{% codeblock %}
    function init() {
		var a = [];
		for(var i=0;i<1000000;i++){
			a.push(i);
		}
		return a;
	}
	function testforEach(arr){
		arr.forEach(function(e){arr[e]});
	}
	function testfor(arr) {
		for(var i = 0; i<arr.length;i++){
			arr[i];
		}
	}
	function testfor2(arr) {
		for(var i = 0,len=arr.length; i<len;i++){
			arr[i];
		}
	}
	function testforIn(arr){
		for(var i in arr) {
			arr[i];
		}
	}
	function testmap(arr) {
		arr.map(function(value,index,arr){arr[index]});
	}
	function testforOf(arr){
		for(let index of arr){
			arr[index]
		}
	}
	window.onload = function(){
		var arr = init();
		console.time("forEach");
		testforEach(arr);
		console.timeEnd("forEach");
		console.time("for");
		testfor(arr);
		console.timeEnd("for");
		console.time("for2");
		testfor2(arr);
		console.timeEnd("for2");
		console.time("forIn");
		testforIn(arr);
		console.timeEnd("forIn");
		console.time("map");
		testmap(arr);
		console.timeEnd("map");
		console.time("forof");
		testforOf(arr);
		console.timeEnd("forof");
	}
	{% endcodeblock %}
### 性能分析
代码运行时间：
forEach: 13.323974609375ms
for: 1.428955078125ms
for2: 1.48583984375ms
forIn: 160.415771484375ms
map: 155.574951171875ms
forof: 5.385009765625ms

分析：
1.经过大量数据测试，普通的for循环是速度最快的
2.优化的for循环速度和for循环速度差不多，甚至更快一点，因为初始化length之后，就不必每次都去查询长度了。
3.forEach 的缺陷在于ie不支持
4.for..in,看上去和for循环差不多，但是差别很大，每次遇到for..in循环时，需在后台创建一个枚举器，enumerator，所以导致速度很慢
5.map方法创建一个新数组，返回结果是该数组中的每个元素都调用一个提供的函数后返回的结果。参数是一个回调函数，回调函数的三个参数分别是value,index,arr
6.for..of es6之后才能使用。

----
 代码地址：https://github.com/zthappy/Javascript.git
 运行：http://htmlpreview.github.io/?https://github.com/zthappy/Javascript/blob/master/Array/arraycycle.html


