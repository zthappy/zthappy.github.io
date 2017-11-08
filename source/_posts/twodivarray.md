---
title: 二维数组相关
date: 2017-07-13 19:13:21
tags: js
---
## 二维数组
 二维数组是指一维数组的每个元素也是一个数组。同理可以得出三维数组，多维数组的形式。
### 二维数组的生成
1.直接定义，适用于已知的并且比较简单的二维数组
    <pre>var arr = [[1,2,3],[4,5,6]];</pre>
2.循环定义
    <pre>var arr = [];
    for(var i = 0; i < n ; i++){
        arr[i] = [];
        for(var j = 0;j<m;j++){
            arr[i][j] = value;
        }
    }
    </pre>
其中，n,m分别代表数组的宽度和深度。
遍历也是如此遍历
### 二维数组与一维数组的相互转换
   ##### 二维 => 一维
    function toArr(arr){
        var arr1 = [];
        for(var i = 0;i<arr.length;i++) {
            for (var j = 0; j < arr[i].length; j++) {
                arr1.push(arr[i][j]);
            }
        }
        console.log(arr);
        console.log(arr1);
        return arr1;
    }
##### 一维 => 二维
    function toMatrix(i,j,arr){
        var arr1 = [];
        for(var k = 0;k<i;k++){
            arr1[k] = new Array();
            for(var t = 0;t<j;t++) {
                arr1[k][t] = arr[k*i+t];
            }
        }
        console.log(arr1);
        return arr1;
    }
二维数组对应一维数组的对应关系是 a[i][j] = b[i*arr[0].length+j];
### 二维数组的螺旋遍历
    function helix(arr){
        var start_x = 0,end_x = arr.length-1;
        var start_y = 0,end_y = arr[0].length - 1;
        console.log(start_x+","+end_x+","+start_y+","+end_y)
        while(start_x <= end_x && start_y<= end_y) {
            var i;
            var str1="",str2="",str3="",str4="";
            for(i=start_y;i<=end_y;i++){
                str1 += arr[start_x][i]+" ";
            }
            console.log(str1);
            start_x++;
            for(i=start_x;i<=end_x;i++){
                str2 += arr[i][end_y]+" "
            }
            console.log(str2);
            end_y--;
            for(i=end_y;i>=start_y;i--){
                str3 += arr[end_x][i]+" ";
            }
            console.log(str3);
            end_x--;
            for(i=end_x;i>=start_x;i--){
                str4 += arr[i][start_y]+" ";
            }
            console.log(str4);
            start_y++;
        }
    }
    设计思路，设置一个x方向的头和尾，y方向的头和尾，每当走到尾，则换方向。

----
代码地址：https://github.com/zthappy/Javascript/blob/master/Array/twodiarray.html
运行：http://htmlpreview.github.io/?https://github.com/zthappy/Javascript/blob/master/Array/twodiarray.html