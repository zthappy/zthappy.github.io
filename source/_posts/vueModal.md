---
title: js对象相关
date: 2017-08-02 14:00:01
tags: js
---

对象的拷贝

深拷贝和浅拷贝

实现深拷贝
<pre>
var cloneObj = function(obj){
    var str, newobj = obj.constructor === Array ? [] : {};
    if(typeof obj !== 'object'){
        return;
    } else if(window.JSON){
        str = JSON.stringify(obj), //系列化对象
        newobj = JSON.parse(str); //还原
    } else {
        for(var i in obj){
            newobj[i] = typeof obj[i] === 'object' ?
            cloneObj(obj[i]) : obj[i];
        }
    }
    return newobj;
};
</pre>

