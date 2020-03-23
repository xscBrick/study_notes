# Study_php_核心编程

[TOC]

## 表单传值

表单传值即浏览器通过表单元素将用户的选择或者输入的数据提交给后台服务器语言。
为什么使用表单传值
动态网站（Web2.0）的特点就是后台根据用户的需求定制数据，所谓的“需求”就是用户通过当前的选择或者输入的数据信息，表单就是这些数据的承载者。

表单传值方式

### GET传值

1）**form表单**

**<form method="GET">表单元素</form>**

2）**a标签**
<a href=”www.itcast.cn/index.php?学科=PHP”>
3）**location对象的href属性**

<script>location.href=”www.itcast.cn/index.php?data=PHP”</script>
4）**location对象的assign()方法**

<script>location.assign(“www.itcast.cn/index.php?data=PHP”)</script>
### POST传值

1）post表单方式的基本设定

<form method="POST">表单元素</form>
2）post方式跟get方式的区别

1、 Get传输的数据主要用来获取数据，不改变服务器上资源：get只是用来获取内容

2、 Post传输的数据主要用来增加数据，改变服务器上资源：POST会改变服务器上数据内容

3、 传输方式上post必须使用form表单，而get可以使用form表单和URL

4、 get传输数据可以在URL中对外可见，而post不可见：GET传值最终会在浏览器的地址栏中全部显示：?数据名=数据值&数据名2=数据值2…

5、 get和post能传输的数据大小不同，get为2K，post理论无限制（事实上，GET和POST本身没有数据长度限制，但是浏览器厂家做了一些限制）

6、 get和post能够传输的数据格式有区别：get传输简单数据（数值/字符串），post可以提交复杂数据（二进制等）

## PHP接收数据的三种方式 get, post,request

不管是$_GET, $_POST, $_REQUEST，三个都是PHP超全局（没有范围限制）预定义数组，表单元素的“name”属性的值作为数组的下标，而value属性对应的值就是数组的元素值

$_GET方式：接收GET方式提交的数据

$_POST方式：接收POST方式提交的数据

$_REQUEST方式：接收POST或者GET提交的所有数据

1）$_REQUEST所存储数据的内容：将$_POST和$_GET合并存储到一个数组

2）$_REQUEST和$_POST与$_GET的联系：如果GET和POST中有同名数组元素（下标），POST会覆盖GET（PHP中数组元素下标具有唯一性），这个可以在php.ini中进行配置

GET/POST/REQUEST关系

```php
<?php
    echo '<pre>';
    var_dump($_GET);
    echo '<hr>';
    var_dump($_POST);
    echo '<hr>';
    var_dump($_REQUEST);

?>
```

![1571665962086](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571665962086.png)

证明在REQUEST中POST会覆盖GET

![1571666074901](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571666074901.png)

### PHP处理复选框数据 checkbox

复选框表单项的命名方式
复选框：通常是将一类内容以同样（同名）的形式传递给后台，数据库存储通常是一个字段存储。复选框的特点：选中才会提交

1、	在浏览器端，checkbox的name属性的值不论什么都会被浏览器毫无保留的提交
2、	在PHP中 **$_POST** / **$_GET** 都会对同名name属性进行覆盖

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>test_checkbox</title>
</head>
<body>
    <form action="checkbox_test.php" method="post">
        <input type="checkbox" name="hobbby[]" value="basketball">basketball
        <hr>
        <input type="checkbox" name="hobbby[]" value="football">football
        <hr>
        <input type="checkbox" name="hobbby[]" value="pingpang">pingpang
        <hr>
        <input type="submit" name="btn" value="提交"/>
    </form>

</body>
</html>
```

```php
<?php

//接收checkbox数据
header('Content-type:text/html;charset=utf-8');	//告诉浏览器当前服务器返回的内容是text/html，同时需要浏览器用utf-8字符集解析
echo '<pre>';
print_r($_POST);
echo '</pre>';
```

![1571667043478](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571667043478.png)

解决方案：浏览器不识别[]（浏览器不认为有特殊性），但是PHP认为[]有特殊性：系统自动认为该符号是数组的形式，所以PHP就会自动的将同名的但是带有[]的元素组合到一起形成一个数组

## PHP处理复选框数据

### 复选框数据的常见处理

#### 1）单选按钮的数据处理

Radio button：可以出现多个选择项，但是只能选择其中一个

1、 表单中使用的name属性，使用同名即可：只能选中一个

2、 后台接收数据也不需要额外处理

3、 数据库存储的话只需要一个字段存储普通数据即可（数字或者字符串）

4、 PHP拿到数据之后，组织SQL直接存储到数据表即可

```html
<input type="radio" name="gender" value="1" checked="checked" /> 男
<input type="radio" name="gender" value="1" /> 女
```

#### 2）多选按钮的数据处理

1、	表单中name属性使用数组格式：名字[]（一类复选框数据使用一个）
2、	后台接收到数据之后，是一个数组（数组不能存储到数据库）
3、	PHP需要将数组转换成指定格式的字符串：使用分隔符分隔每一个元素并且形成字符串：implode(’分隔符’ ,数组)
4、	PHP组织SQL直接存储到数据库

```php
$hobby_string = implode($hobby, '|');
echo $hobby_string;
```

#### 取出来复选框数据显示

1、	如果是反过来操作，那么取出数据之后使用explode把字符串变成数组

2、	在HTML显示当中，通过判断复选框元素是否在数组中存在，来确定复选框checkbox是否有checked=“checked”属性：in_array()

3）其他常规同名表单项的数据处理
除开radio button单选框和checkbox复选框，很少会出现同名的表单项。如果非要使用同名的来进行管理，那么可以采用checkbox方式进行操作
1、	表单中同名增加[]
2、	PHP接收时数组处理
3、	PHP转换成有格式的字符串
4、	数据库字符串存储

#### 复选框细节

如果复选框没有选中，那么浏览器就不会提交。因此在PHP接收使用复选框（单选框）数据的时候，应该先判断是否存在该数据

```php
<?php

//接收checkbox数据
header('Content-type:text/html;charset=utf-8');	//告诉浏览器当前服务器返回的内容是text/html，同时需要浏览器用utf-8字符集解析
$hobby = isset($_POST['hobby']) ? $_POST['hobby'] : array();
$hobby_string = implode($hobby);
'<pre>';
print_r($hobby_string);
```

# 文件上传

##### 原理

文件上传：文件从用户本地电脑通过传输方式（Web表单）保存到服务器所在电脑指定的目录下。

 

1、 增加文件上传的表单：浏览器请求一个服务器的HTML脚本（包含文件上传表单）

2、 用户从本地选择一个文件（点击上传框（按钮））

3、 用户点击上传：文件会通过物联网传输到服务器上

4、 服务器操作系统会将文件保存到临时目录：是以临时文件格式保存（windows下tmp）

5、 服务器脚本开始工作：判断文件有效

6、 服务器脚本将有效文件从临时目录移动到指定的目录下（完成）

![1571752808101](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571752808101.png)

## 表单写法

1）method属性：表单提交方式必须为POST

2）enctype属性：form表单属性，主要是规范表单数据的编码方式

![1571752894512](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571752894512.png)

上传表单：file表单

```html
<body>
    <form method="post" enctype="multipart/form-data" action="file_upload.php">
        <input type="file" name="image" />
        <input type="submit" name="btn" value="上传文件" />

    </form>
</body>
```

在PHP中，有一个预定义变量$_FILES是专门用来存储用户上传的文件的。

## $_FILES变量详解

1）name：文件在用户（浏览器端）电脑上实际存在的名字（实际用来保留后缀）

2）tmp_name：文件上传到服务器后操作系统保存的临时路径（实际用来给PHP后期使用）

3）type：MIME（多功能互联网邮件扩展）类型，用来在计算机中客户端识别文件类型（确定软件）

4）error：文件上传的代号，用来告知应用软件（PHP）文件接收过程中出现了什么问题（PHP后期根据代码进行文件判断）

![1571753893595](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571753893595.png)

5）size：文件大小（PHP根据实际需求来确定是否该保留）

## 移动临时文件到目标位置

文件上传之后会保存到$_FILES中，那么访问文件信息的形式就是$_FILES[‘ 表单name属性值’][‘元素信息’]

1）判断是否为上传的文件：is_uploaded_file()

```php
//1.取得文件信息
$file = $_FILES['image'];
//判断文件是否是上传文件，临时文件
if(is_uploaded_file($file['tmp_name'])){
	//是上传文件
}else{
    echo '文件上传失败';
}
```

2）移动文件：move_uploaded_file()

```php
//1.取得文件信息
$file = $_FILES['image'];
//判断文件是否是上传文件，临时文件
if(is_uploaded_file($file['tmp_name'])){
	//是上传文件
    if(move_uploaded_file($file['tmp_name'], 'uploads/'.$file['name'])){
        echo '文件保存 成功';
    }
}else{
    echo '文件上传失败';
}
```

## 多文件上传

当商品需要上传多个图片进行展示的时候：那么需要使用多文件上传

​    针对一个内容但是不同文件说明：同名表单

```html
<form method="POST" enctype='multipart/form-data' action="multi_upload.php">
    <input type="file" name="image[]" />
    <input type="file" name="image[]" />
    <input type="file" name="image[]" />
    <input type="submit" name="btn" value="batch_upload" />
</form>
```

```php

```

当商品需要进行多个维度图片说明的时候：需要使用多文件上传

​    针对是不同内容所以表单名字不一样：批量解决问题