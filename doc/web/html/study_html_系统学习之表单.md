# study_html_系统学习之表单 form

[TOC]

表单它主要是用来手机用户输入的相关数据

注意：	

​	一个完整的表单，是由 form 标签 和表单控件标签 组成

```
action 属性	将 表单的数据提交给谁，进行处理
			如果 form 标签没有写 action 属性，则表示将表单数据提交给当前的本页面进行处理
target 属性	规定在何处打开 action URL
enctype	multipart
```



如果实现文件上传功能， form 标签里面由两个属性必须要设置

第一个 method 属性值要为post

第二个：enctype 的属性值 为 multipart/form-data

```
<form action="" enctype="multipart/form-data" method="POST">
	<label for="upload">上传文件</label><input type="file" id="upload" name="user"><br>
</form>
```



## input 功能标签

属性：

```
type	text文本|file，submit，password
name 
value	用户输入属性
disable	禁用，这个属性没有属性值，它的值等于本身
readonly


```

disable&readonly	如果使用了 disabled 的输入框，这个输入框里面的内容不会发送给服务器，readonly 可以发送给服务器



type属性

```
radio	// 单选按钮，name属性值必须是一样的，如果是单选钮或者复选框，必须设置value 属性值，
checkbox	复选按钮
text
file
submit
```

### 单选框

单选按钮，name属性值必须是一样的，如果是单选钮或者复选框，必须设置value 属性值，checked 属性

```

```



## cookies

### label 

```
<label for="username">用户名：</label><input type="text" id="username"><br>
```

for 属性，关联对应控件标签的 id属性的值