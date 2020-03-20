# study_php_系统学习之核心编程

[TOC]

## 会话技术

### cookie

类似于会员卡功能

服务器端，将能够唯一标识用户的数据保存客户端的一种方式，之后浏览器在每次请求时都会自动携带给服务器



#### 设置cokkie

```php
<?php
header('set-cookie:id=10');
setcookie('name', 'zhang');
```

setcookie(name, value[, expire[, path[, domain[, secure[, httpponly]]]]]);

name	就是cookie名

value 	就是cookie 值

位于客户端的cookie 的本质就是文本文件

#### 读取cookie

$_COOKIE	就是一个关联数组，主要是用于存储客户端通过 cookie 的技术，提交的数据



#### cookie的有效时间 expire

expire 是用于设置 cookie 的过期时间，时间是以秒记录的，有效期的起点是时间原点

​	如果省略，表示会话cookie，有效期到浏览器关闭

#### cookie 的路径

setcookie(name,value,expire,path)

首先明确：	

​	php 文件有自己位于服务器上的路径

说明：

​	path 	是用于设置 cookie 在浏览器端显示的路径

​	默认当客户端访问某一个 php 文件时，究竟什么样的cookie 会被携带给服务器，其中 cookie 的显示路径就可以决定是携带给所请求的 php 文件

​	如果客户端的 cookie 的显示路径是所请求的 php 文件路径的父路径则会携带过去，但是绝大多数情况我们是将一个 cookie 设置为整站有效('path' = '/')

```php
setcookie('name','zhangsan',time()+30,'/'); //cookie 整站有效
```



#### cookie 的域



## 搭建项目



主机搭建

创建虚拟主机

![image-20200215164233038](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200215164233038.png)

创建域名解释器

127.0.0.1  www.news.com



### 创建画布：imagecreatetruecolor(w,h)

w	标识的是所要创建的画布宽

h	表示所要创建的画布高



```
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w, $h);

header('content-type:image/jpeg');
imagejpeg($img);
```

### 创建画布颜色 imagecolorallocate(img,r,g,b);

说明：

​	img 	画布资源/gd资源

​	rgb	十进制的颜色表示方法

​	此函数仅是创建了一个颜色资源，但并没有使用

```php
//创建画布
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w, $h);

//2.分配颜色，创建颜色
$bg = imagecolorallocate($img, 255, 0, 0);

header('content-type:image/jpeg');
imagejpeg($img);
```

#### 填充颜色 imagefill(img, x, y, color);

语法：

​		imagefill(img, x, y, color);

```
//创建画布
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w, $h);

//2.分配颜色，创建颜色
$bg = imagecolorallocate($img, 255, 0, 0);

//3.填充颜色
imagefill($img, 0, 0, $bg);

header('content-type:image/jpeg');
imagejpeg($img);
```

# 前后台数据的提交



get

get 方式是将表单元素的 name 属性值与用户输入的数据，组织成对的形式，放在url 传递到所请求的文件

```php
<form action="form_get.php" method="GET">
    <label for="name">用户名:<input type="text" name="name" id="name"></label><br/>
    <label for="pwd">密码:<input type="password" name="pwd" id="pwd"></label><br/>
    <input type="submit" name="提交">
</form>
```

post 

post 方式将用户输入的数据，与表单元素的 name 属性值，组织成对对的形式，将数据放在 http 协议内部，传递到后台

```html
//cokies
使用label 关联， for属性关联对应的 id值
```

```
<form action="form_get.php" method="POST">
        <label for="name">用户名:<input type="text" name="name" id="name"></label><br/>
        <label for="pwd">密码:<input type="password" name="pwd" id="pwd"></label><br/>
        <input type="submit" name="提交">
    </form>
```

模拟get 方式提交数据

主要应用在没有表单的情况下，向后台提交数据

如何模拟：只要是html文档中能够输入url的地方，在所请求的文件名后 加 ? 名=值&名=值 方式

```
<a href=""><a/> //php文件
window.location.href=url; 	//php文件，js
```



```
table>thead>tr>th**4^^tbody>tr>td**4	
```

```
 <table border="1" rules="all">
        <thead>
            <tr>
                <th>序号</th>
                <th>商品</th>
                <th>价格</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td >1</td>
                <td>mate</td>
                <td>4000</td>
                <td><a href="form_post.php?id='1'">删除</a></td>
            </tr>
            <tr>
                <td>2</td>
                <td>mate 10</td>
                <td>5000</td>
                <td><a href="form_post.php?id='2'">删除</a></td>
            </tr>
        </tbody>
    </table>
```



#### 后台数据的接收

$_GET

用于接收前台使用get 方式(get & 模拟get(a 标签))提交的数据

$_POST

$_REQUEST

#### 特殊表单的提交

对于复选框，在设置html 时，需要在 name 属性值的后面加[], 这个'[]' 符合一旦被php接收后，会自动转换为数组

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=for, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form action="request.php" method="post">//action 接收数据的文件
        <label for="name">用户名：<input type="text" name="name" id="name"></label><br/>
        <label for="pwd">密码：<input type="password" name="pwd" id="pwd"></label><br/>
        <label for=""><input type="checkbox" name="color[]" value="red">红色</label>
        <label for=""><input type="checkbox" name="color[]" value="yellow">黄色</label><br/>
        <label for=""><input type="checkbox" name="color[]" value="white">白色</label>
        <label for=""><input type="checkbox" name="color[]" value="blank">黑色</label><br/>
        <input type="submit" name="submit"><br/>
    </form>
</body>
</html>
```



### 文件上传原理

#### 1. 前台部分

form 表单：

​	action 属性应该指向一个php 文件

​	method 属性必须设置为post

​	enctyoe 属性：

​		取值：		
​				application/x-www-url-encoded	(默认)只能上传文本数据
​				multipart/form-data			可以上传多种类型文件

```
<form action="" method="POST" enctype="multipart/form-data">
<label for="myfile">上传文件：<input type="file" name="myfile" id="myfile"></label><br>
<input type="submit" value="submit">
</form>
```



#### 2. 后台处理

上传的文件被保存在 $_FILES 这个数组中

#### 3. 文件上传的原理

更改临时文件夹：

```
//php.ini
upload_tmp_dir = d:/tmp //临时缓存文件存储文件夹
```

重新启动 apache

临时文件中的文件，在php 脚本执行结束后会被自动删除。 所以文件上传的原理就是将位于临时文件夹中的临时文件，移动到其他位置



语法：

​	move_uploaded_file(tmp,dest);

说明：

​	tmp 	用户上传的临时文件

​	dest	目标文件

```php
<?php
echo "<pre>";
$tmp = $_FILES['myfile']['tmp_name'];
$dest = 'C:/software/phpstudy/phpstudy_pro/WWW/core_programming/files/';
$dest .= $_FILES['myfile']['name'];
move_uploaded_file($tmp,$dest);
```

#### 4. 完善上传文件

控制文件的大小

控制文件的格式

控制文件的保存的文件名

1. 生产随机文件名

   mt_rand(m, n)	生成 m 与 n 之间的随机整数

   chr(code)	将 code 所表示的整数转化为响应的字符

![image-20200222161651421](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200222161651421.png)

```php
<?php
echo "<pre>";
$tmp = $_FILES['myfile']['tmp_name'];
$dest = 'C:/software/phpstudy/phpstudy_pro/WWW/core_programming/files/';
// $dest .= $_FILES['myfile']['name'];//原始文件名
//随机文件名
$fileName = getFileName();
$dest .= $fileName;
//获取文件扩展名
$info = pathinfo($_FILES['myfile']['name']);
$dest .= '.' . $info['extension'];
/*Array
(
    [dirname] => .
    [basename] => 12.9徐三春  加急加急  修改.docx
    [extension] => docx
    [filename] => 12.9徐三春  加急加急  修改
)
 */
//获取随机一组6个字符用以作为文件名
function getFileName(){
    $string = '';
    for($i=0; $i<6;$i++){
        switch(mt_rand(0,2)){
            case 0:
                $string .= chr(mt_rand(65,90));
                break;
            case 1:
                $string .= chr(mt_rand(97,122));
                break;
            case 2:
                $string .= mt_rand(0,9);
                break;
        }
    }
    return $string;
}
// print_r($fileName);
move_uploaded_file($tmp,$dest);
```

2. 控制允许上传的文件的类型

   通过

   ```php
   //定义允许用户传的 mime 类型
   $mime = ['image/jpeg', 'image/jpg', 'image/pjpeg', 'image/png', 'image/gif'];
   if(!in_array($_FILES['myfile']['type'], $mime)){
       exit('文件类型不合法！');
   };
   
   ```

3. 控制文件的大小



4. 判断文件上传过程中的错误信息

   ```php
   switch($_FILES['myfile']['error']){
       case 1:
           exit('文件超过 php.ini限制');
           break;
           
       case 2:
           exit('文件超过 html 限制');
           break;
       case 3:
           exit('文件上传不完整');
           break;  
   	case 4:
           exit('没有选择文件');
           break;
   	case 6:
           trigger_error('');
           exit('服务器内部错误');
           break;
   	case 7:
           exit('服务器内部错误');
           break;
   }
   ```

   

#### 6. 文件上传的相关配置

1. 开启文件上传

```php+HTML
;Whether to allow HTTP file uploads.
file_uploads = On
```

2. 设置临时文件夹

```php
upload_tmp_dir = c:/tmp
```

3. 设置文件上传的最大大小

```php
upload_max_filesize = 2M
```

4. 设置文件一次最多可以上传多少个文件

```php
max_file_uploads = 20
```

5. post 方式提交数据最大的大小

```
post_max_size = 8M
```



# 搭建项目



## php 操作数据库

### 1. 连接数据库

 mysqli_connect(host, user, pwd);

如果成功，返回的是一个 对象 obj

如果失败，返回的是false





## 文件管理

### 文件操作

PHP 也提供了一套文件操作系统函数，通过这套函数进行文件管理，创建文件，删除，改名，存储数据，读取数据

文件的理解：在文件管理系统分为两种：文件&文件夹



#### 文件相关信息

1. file_exists(filename);
   判断一个文件是否存在

   ```
   
   ```

   

2. filemtime(filename);

   用于获取文件修改的时间(返回时间戳)

   ```
   filemtime($filename);
   ```

   

3. filesize($filename);  字节

4. basename($filename);

   



# curl

Command Url

Curl 是一个代码版的浏览器，允许我们在代码中像使用浏览器一样访问别人的页面

默认 php 并没有开启对 curl 的支持，需要我们在配置文件中手动开启

```
extension=php_curl.dll
```

提示：
	如果开启后也无法使用，需要将php 目录中的三个文件 libeay32.dll,  libssh2.dll, ssleay32.dll, php5ts.dll, 文件复制到 apache 的bin 目录内



## curl 函数的使用

### 1. curl 的初始化(打开一个浏览器)

```php
$ci = curl_init(); //返回的是 curl 资源类型
```



### 2. 设置curl 选项(输入地址)

```
curl_setopt($ci, CURL_URL,'http://www.baidu.com');  
```

curl_setopt(curl，参数名，参数值);

​	curl	就是curl_init 的返回值

​	参数名	参数都是以常量的形式设计的

​	CURLOPT_URL 	用于设置所请求的网址

​	CURLOPT_RETRUANTRANSFER	取值如果是1，表示不讲接收到的数据直接返回给浏览器，而是作为 curl_exec()的 返回值

```
curl_setopt($ci, CURL_URL,'http://www.baidu.com');  
curl_setopt($ci, CURLOPT_RETRUANTRANSFER,1);
```



### 3. 执行 curl (回车)

用于执行某个curl工具

```
curl_exec(curl);
```



#### 4. 模拟get 请求

```php
//1.初始化
$ci = curl_init();
//
$url = 'www.news/php/delnews.php?id=1';
curl_setopt($ci, CURLOPT_URL, $url);
curl_setopt($ci, CURLOPT_RETRUANTRANSFER,1);
//运行
curl_exec($ci);
```



### 5. 模拟post 请求

CURLOPT_POST	取值为1

CURLOPT_POSTFIELDS

```php
//1.初始化
$ci = curl_init();
//2.设置url 选项
$url = 'www.news/php/insert.php';
curl_setopt($ci, CURLOPT_URL, $url);
curl_setopt($ci, CURLOPT_RETRUANTRANSFER,1);
//设置post请求方式
curl_setopt($ci, CURLOPT_POST,1);

//定义数据
$data = ['n_title'=>'^^',];
curl_setopt($ci, CURLOPT_POSTFIELDS,$data);

//运行
curl_exec($ci);
```

