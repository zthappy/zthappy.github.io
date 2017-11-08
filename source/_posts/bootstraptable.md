---
title: bootstraptable使用总结
date: 2017-07-17 17:51:13
tags: bootstrap
---
### bootstrap常用的一些
1.接口返回格式不是默认格式时：
<pre>
    responseHandler:function (res) {
        return res.Data;
    }
</pre>
2.复选框全选，不选
<pre>
    checkbox: true,
    formatter: function (value, row, index) {
        if (row.TFGSSyncStatus != 99){
            return {
                disabled: true,
                checked: false
            }
        }
    }
</pre>
js中
<pre>
     var dataItem = $('#financeNewList').bootstrapTable("getSelections");
        angular.forEach(dataItem, function (e, i) {
            var para = {
                OrderSerialId: e.TFGSOrderSerialId,
                Id: e.DbrGuid,
            };
            paras.push(para);
        });
        </pre>
        这边是用了angular的循环，可以自己替换成其他的循环
3.常用属性
<pre>
     url: '/BackendTasks/GetAllTasks', //请求后台的URL（*）
     method: 'get', //请求方式（*）
     toolbar: '#toolbar', //工具按钮用哪个容器
     striped: true, //是否显示行间隔色
     cache: false, //是否使用缓存，默认为true，所以一般情况下需要设置一下这个属性（*）
     pagination: true, //是否显示分页（*）
     sortable: true, //是否启用排序
     sortOrder: "asc", //排序方式
     queryParams: oTableInit.queryParams, //传递参数（*）
     sidePagination: "server", //分页方式：client客户端分页，server服务端分页（*）
     pageNumber: 1, //初始化加载第一页，默认第一页
     pageSize: 5, //每页的记录行数（*）
     pageList: [10, 25, 50, 100], //可供选择的每页的行数（*）
     search: false, //是否显示表格搜索，此搜索是客户端搜索，不会进服务端，所以，个人感觉意义不大
     strictSearch: true,
     showColumns: true, //是否显示所有的列
     showRefresh: true, //是否显示刷新按钮
     minimumCountColumns: 2, //最少允许的列数
     clickToSelect: true, //是否启用点击选中行
     height: 500, //行高，如果没有设置height属性，表格自动根据记录条数觉得表格高度
     uniqueId: "Id", //每一行的唯一标识，一般为主键列
     showToggle: true, //是否显示详细视图和列表视图的切换按钮
     cardView: false, //是否显示详细视图
     detailView: false, //是否显示父子表
</pre>


3.表单验证之复选框
angular自带了表单验证,比如
<pre>
    &lt;div class="col-lg-24"&gt;
        &lt;input type="text" ng-model="para.TFPRSupplierId" class="form-control" name="TFPRSupplierId"  id="TFPRSupplierId" required/&gt;
    &lt;/div&gt;
    &lt;span class="validation"&gt;
        &lt;font ng-show="myForm.TFPRSupplierId.$error.required"&gt;*&lt;/font&gt;
    &lt;/span&gt;
</pre>
一般的下拉框，input都可以用表单验证，在提交的按钮里myForm.$error.required即可，这是必填，还可以结合过滤器等验证其他，比如金额等
但是复选框，angular没有实现
于是，我再一次偶然的开发中做到了简单的验证复选框必选
代码如下：html
<pre>
    &lt;div class="col-lg-24"&gt;
    &lt;label ng-repeat="item in initData.PayOrderType"&gt;&lt;input type="checkbox" name="payorderType" value="{{item.Value}}" ng-click="isSelected($event,item.Value)"&gt;{{item.Text}}&lt;/label&gt;
    &lt;/div&gt;
    &lt;span class="validation"&gt;
        &lt;font ng-show="status"&gt;*&lt;/font&gt;
    &lt;/span>
</pre>
js
<pre>
$scope.status = true;
var arr = [];
$scope.isSelected = function(e,item) {

    if(e.target.checked == true) {
        arr.push(item);
    }
    else {
        arr.splice(arr.indexOf(item),1);
    }
    if(arr.length > 0){
        $scope.status = false;
    }
    else {
        $scope.status = true;
    }
}
</pre>
