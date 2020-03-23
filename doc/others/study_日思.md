# study_日思

[TOC]

## 2019/11/14

html代码

```html
<div class="tab_list_body_item vbc_transfer">
    <div style="padding-top: 10px; padding-bottom: 10px" class="search_vbc_transfer">
        <h4>查询条件</h4>
        <span>地域：</span> <select class="span2 ccn_region_info_j regionId"></select></span>
        <span>ccn id：</span><input class="vbcId" type="text" placeholder="ID">
        <span>ccn唯一id：</span><input class="uniqVbcId" type="text" placeholder="">
        <span>AppId：</span><input class="owner" type="text" placeholder="请输入appId" value="<?php echo $appId;?>">
        <span>网关集群ID：</span><input class="vbcgwId" type="text" placeholder="请输入网关集群id">
        <span>网关集群唯一ID：</span><input class="uniqVbcgwId" type="text" placeholder="请输入网关集群唯一id">
        <span>网关vip：</span><input class="gwIp" type="text" placeholder="请输入网关vip">                 		</div>
</div>
```

js代码

```js
var exportTransferVbcInstanceList = function(){
    var param = {};
    var _v = '';
    $.each(['vbcId','uniqVbcId', 'owner', 'regionId','vbcgwId','uniqVbcgwId','gwIp'],function(i,k){
        var _v = $.trim($('.vbc_transfer .search_vbc_transfer .'+k).val());
        if (_v !== '') {
            param[k] = _v;
        }
    });
    var url = CGI_EXPORT_URL + 'exportVbcTransferList';
    document.location.href = url + "?" + $.param(param);
};
```

mysql数据库中不现实中文，中文变成了‘？？？’’

原因分析：可能是数据库的编码出现了问题。

进入数据库 mysql -u root -p 

```
1.mysql>>show databases;
2.mysql>>show variables like ‘char%’;#查看数据库的编码
3.mysql>> set character_set_results=utf8;#改变编码方式
```

2019/11/16

1. 表单控件
	1. 文本框与密码框
	2. 单选钮和复选框
	3. 下拉菜单,文本域
	4. 隐藏域,文件选择框
	5. 提交,重置,普通按钮
2. CSS使用
	1. 引入方式
		内联 : style属性 style="color:red;"
		内嵌 : <style>
							选择器{}
					 </style>
		外链 : 创建.css文件
					 在HTML中引入<link rel="" href="" type="">
		优先级 :
			1. 内联样式优先级最高
			2. 内嵌与外链优先级相同,发生冲突时后来者居上
	2. 样式表特征
		1. 层叠性
		2. 继承性
		3. 优先级
	3. 选择器
		1. 标签选择器
		2. id选择器 #id属性值
		3. class选择器 .class属性值
		4. 群组选择器
				选择器1,选择器2{}
		5. 后代选择器
				选择器1 选择器2{}
		6. 子代选择器(直接子元素)
				选择器1>选择器2{}
		7. 伪类选择器
				:link
				:visited
				:hover
				:active
				:focus
	4. 选择器的优先级
			标签选择器		1
			类选择器			10
			id选择器			100
			行内样式			1000

		 复杂选择器(后代,子代等)的优先级由各个选择器的权重值相加得到
		 例 :
				h1{} 
				.c1{}
				#d1{}
				div h1{}   2
				div .c1{}  11
				div #d1{}
				#d1 .c1{}
	5. 标签分类
			1. 块元素
				独占一行;可以手动设置宽高,默认宽度与父元素保持一致. 例 : div h1 p ul ol li table form
			2. 行内元素
				可与其他元素共行显示;不能手动设置宽高
				例 : span label b strong i s u sub sup a
			3. 行内块元素
				既可以共行又可以设置宽高
			标签嵌套 :
				1. 块元素中可以嵌套任意类型的元素
						p元素中只能嵌套行内(块)
				2. 行内元素可以嵌套行内(块元素)

### css 颜色

英文单词/rgb / 	rgb，alpha / 十六进制

rgb：使用三原色表示，每种颜色取值范围为 0-255 值越大越饱和

rgba：alpha 表示透明度，0(透明)~1(不透明)



## 11/18

js弹出消息对话框的几种方式

```html

<script type="text/javascript">
    //直接弹出，无取消按钮    
   	alert("alert");
    //有取消按钮
   	confirm("Confirm");
    //弹出输入框
   	prompt("prompt");
    //未知
   	document.write("document.write");
    //写入控制台 F12 查看
   	console.log("console.log"); 
</script>
```

