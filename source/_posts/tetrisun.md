---
title: tetrisun
date: 2017-09-13 17:25:55
tags: js
---
### js 实现 俄罗斯方块
俄罗斯方块陪我度过了童年时光，所以在从事了前端之后，一直想用js实现一个俄罗斯方块
下面是我一步步实现俄罗斯方块的步骤

#1.实现背景的控制格
思路：
第一个方法 背景图片
第二个方法 表格
第三个方法 div做成表格
最后我采用了表格的方法，因为表格可以有table.rows[i].cells[j]这个属性，可以直接定位
其次就是表格定义的css比较简单
<pre>
    #bg td {
        width: 20px;
        height: 20px;
    }
</pre>

#2.实现方块
有七种方块，田，山，一，之，L,反L,反之
case 0:{//田
    activeBlock[0] = {x:0, y:4};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:0, y:5};
    activeBlock[3] = {x:1, y:5};
    break;
}
case 1:{
    activeBlock[0] = {x:0, y:3};
    activeBlock[1] = {x:0, y:4};
    activeBlock[2] = {x:0, y:5};
    activeBlock[3] = {x:0, y:6};
    break;
}
case 2:{
    activeBlock[0] = {x:0, y:5};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:1, y:5};
    activeBlock[3] = {x:2, y:4};
    break;
}
case 3:{
    activeBlock[0] = {x:0, y:4};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:1, y:5};
    activeBlock[3] = {x:2, y:5};
    break;
}
case 4:{
    activeBlock[0] = {x:0, y:4};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:1, y:5};
    activeBlock[3] = {x:1, y:6};
    break;
}
case 5:{
    activeBlock[0] = {x:0, y:4};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:2, y:4};
    activeBlock[3] = {x:2, y:5};
    break;
}
case 6:{
    activeBlock[0] = {x:0, y:5};
    activeBlock[1] = {x:1, y:4};
    activeBlock[2] = {x:1, y:5};
    activeBlock[3] = {x:1, y:6};
    break;
}
面板是15*20的表格，所以初始化的时候，“田”字处于第四个方格，同理其他


#3.实现方块的移动
<pre>
//向下
	function moveDown() {
		erase();
		for(let i=0;i<4;i++){
			activeBlock[i].x = activeBlock[i].x+1;
		}
		//console.log(activeBlock);
		updateBg(activeBlock);
		paint();

	}
	//向左
	function moveLeft() {
		erase();
		for(let i=0;i<4;i++){
			activeBlock[i].y = activeBlock[i].y-1;
		}
		//console.log(activeBlock);
		updateBg(activeBlock);
		paint();
	}
	//向右
	function moveRight() {
		erase();
		for(let i=0;i<4;i++){
			activeBlock[i].y = activeBlock[i].y+1;
		}
		//console.log(activeBlock);
		updateBg(activeBlock);
		paint();
	}
</pre>
但是移动的同时还要考虑到 方块的显示，我的方法是，移动一格，就重新绘制一遍
<pre>
//更新背景
function updateBg(activeBlock) {
    for(let i = 0;i<4;i++){
        isBusy[activeBlock[i].x][activeBlock[i].y] =1;
    }
}
//绘制图形
function paint() {
    var table = document.getElementById("bg");
    for (let i =0;i<20;i++){
        for(let j = 0;j<15;j++){
            if(isBusy[i][j] == 1){
                table.rows[i].cells[j].style.backgroundColor = "pink";
            }
        }
    }
}
//擦除
function erase() {
    var table = document.getElementById("bg");
    for (let i =0;i<20;i++){
        for(let j = 0;j<15;j++){
            table.rows[i].cells[j].style.backgroundColor = "white";
            isBusy[i][j] = 0;
        }
    }
}
</pre>