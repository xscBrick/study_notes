# study_php_系统学习之cookie&session

[TOC]

# 会话技术

由于 http 协议是无连接无状态的，所以 http 协议无法记住客户端的信息，为了弥补 http 协议这两点的 "不足" 所以出现了会话技术



## cookie 技术 服务器 会员卡

​	服务器端，将能够唯一标识用户的数据保存客户端的一种方式，之后浏览器在每次请求时都会自动携带给服务器

head('cookie:id=10');





## 读取cookie $_COOKIE

```php
print($_COOKIE);
```



## cookie 设置 setcookie()

### cookie 的有效事件

setcookie(name, value,expire)

expire 是用于设置 cookie 的过期事件，时间是以秒记录的，有效期的起点是时间原点，如果省略表示会话cookie，有效期到浏览器关闭

```php
setcookie('name', 'zhangsan', time()+10);
```



### cookie 的路径

setcookie(name, value,expire, path)

首先明确， php文件有自己位于服务器上的路径

path	用于设置 cookie 在浏览器端显示的路径

​	默认当客户端访问某一个php文件时，究竟什么样的cookie 会被携带给服务器，其中cookie 的显示路径就可以决定是否携带给所请求的文件

​	如果客户端的 cookie 的显示路径是所有请求的 php 文件路径的父路径则会携带过去，但是绝大多数情况我们是将一个 cookie 设置为整站有效

```
setcookie('name', 'zhangsan', time()+3, '/')
```



###  cookie  的域 domain

理解域名，

顶级域名：	主要标识过假

.cn   .us	.jp

一级域名：主要标识行业
.com	商业机构

.gov	政府机构

.org 	非盈利组织

.edu	教育机构

.net	网络机构

.mil	军事机构

二级域名：主要用于标识公司

baidu.com	



cookie 的跨域，只能实现二级域名相同



### cookie  secure

```
setcookie(name,value,erpire,path,domain,secure)
```

secure 	取值为 true 或false

​	如果设置为true 那么只有当客户端使用的协议是 https 时， 则会将 cookie 携带给服务器端



### cookie httponly

true,false

如果设置为 true 那么只有php可以访问，如果false js也可以访问



### 删除cookie

方法1：再设置一次cookie，将其有效期设置为过期(当前日期之前)

方法2：设置cookie的值为空



### 关于 cookie 值得类型



setcookie();	设置cookie

$_COOKIE[]	读取cookie



## seesion 技术 --> 银行卡

### 什么是session

session 也是会话技术中得一种，session 是以 cookie 为基础，将重要得数据保存在服务器端，同时将能够唯一标识这份数据得数据 以cookie 的形式保存客户端 

> 首次请求： 没有携带任何数据
>
> 首次响应：返回数据，以cookie 保存



### 开启 session

session_start();

用于开启 session 机制，同时 激活 $_SEESION 预定于变量



### session 操作 --设置 session

session 的操作就是向 $_SESSION 这个变量中写数据，数组
当向内存中的  $_SESSION  变量中数据时，$_SESSION 变量中数据最终会保存到硬盘(windows-->temp) 的一个文件中

```php
session_start();
//写session，就是向 $_SESSION 这个数组中添加元素
$_SESSION['balance'] = 100; //$_SESSION 是一个变量

```



### session 操作 --读取session

print_r($_SESSION);

当我们从$_SESSION 内存中的变量读取数据，其实是将服务器中那个session 文件中的数据读取到内存中

​	$_SESSION 与 session 文件之间的交互过程

​	首次：服务器首先在硬盘中创建一个唯一的文件，将文件名以cookie 的形式返回给客户端
​		在php 脚本执行结束时，将 $_SESSION 内存变量中的数据写入到 session 文件中

​	其余：请求时，服务器会收到客户端 的 cookie 中保存的 session 文件名，找到对应的 session，并打开这个 session  文件，将文件中的数据读取到 $_SESSION 中

脚本结束时，会重新将 $_SESSION 中的数据写入到 服务器端对应的 session 文件中

### session 操作 -- 获取session ID

```php
session_start();
echo session_id();
```



### session 数据

session 可以存储任何类型的数据，但是 $_SESSION 变量 本身的下标必须是字符串，只能是字符串，不能是数字



### session 销毁

session_destroy()

```php
session_start();
session_destroy();
```



### session 配置

![image-20200308235405404](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200308235405404.png)

用于 设置保存 session 的媒介， 文件还是 session



用于保存 sessionid 的那个 cookie 有效期



![image-20200308235530844](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200308235530844.png)

![image-20200308235640602](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200308235640602.png)



php.ini --> session.save_path = "N; e:/tmp";

​	N 	几级目录 1~9
当项目很大时，会产生 数量非常多的 session 文件，为了能够加快session  文件的查询速度，我们可以采用分目录存储 session 文件

​	session.save_path = "1; e:/tmp";

​	需要在 e:/tmp 目录下需要创建 a-z,0-9 为文件夹名的文件夹36个



### session 垃圾回收机制

session 文件页可以设置一个有效期，默认的设置如下图

![image-20200309223504593](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309223504593.png)

垃圾文件：

​	php 会人为 过期的 session 是一个垃圾文件，所以需要剔除，删除这样的 过期session 文件有一个回收机制

![image-20200309223835928](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309223835928.png)

当 session_start() 开启 session 机制，1000次，有可能触发垃圾回收机制1次，只要垃圾回收机制触发，那所有的过期的 session 文件都会被删除

### cookie 是浏览器的一个功能，也可以被禁止，如果cookie 被进制，如何实现 session

#### 1. 设置不仅仅使用 cookie 保存 sessionid

![image-20200309231949376](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309231949376.png)

#### 2. 设置可以使用 transid 保存 sessionid

![image-20200309232736404](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309232736404.png)



```php
<?php
session_start();
$_SESSION['name'] = 'zhangsan';
?>
<a href="get_user_trans.php">访问服务器</a>
```



```php
//get_user_trans.php
session_start();
echo '<pre>';
print_r($_SESSION);
```

![image-20200309233218908](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309233218908.png)

形成的过程

​	php 在启动的过程中，会检测到 session.use_strans_sid=1,当客户端请求了某个php文件时，session 机制会自动查找当前的 php 文件中是否有 a连接，如果有就在 url 后加 ？PHPSESSION=当前sessionid的值

### 自动开启 session

![image-20200309233917753](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309233917753.png)

![image-20200309234146872](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200309234146872.png)



## 挂脚本共享文件

$_SESSION

同一浏览器进程，共享同一session





## 项目应用

### 登录验证

```php
$u_name = $_POST['uname'];
$u_pwd = $_POST['upass'];

//1. 验证
$obj = mysqli_connect('127.0.0.1', 'root', '123');
$sql = 'set names utf8';
$res = mysqli_query($obj, $sql);

$sql = 'use news_db';
$res = mysqli_query($obj, $sql);

$pwd = md5($password);
$sql = 'select * from where u_name="$uname" and u_pwd="$pwd" limit 1';

$result = mysqli_query($obj, $sql);
$userInfo = mysqli_fetch_assoc($result);
//2. 判断
if($userInfo){
    header('Location:listNews.php');
}else{
    header('Location:login.php');
}
```



### 防止翻墙

登录成功，则设置session，其他文件则验证是否有指定session

```php
$userInfo = mysqli_fetch_assoc($result);//获取结果关联数组
//2. 判断
if($userInfo){
    $_SESSION['userInfo'] = $userInfo;
    header('Location:listNews.php');
}else{
    header('Location:login.php');
}
```



mysqli_fetch_assoc

```
$sql="SELECT name,url FROM websites ORDER BY alexa";
$result=mysqli_query($con,$sql);
 
// 关联数组
$row=mysqli_fetch_assoc($result);
printf ("%s (%s)\n",$row["name"],$row["url"]);
```



### 注销 功能

销毁 session，

1.创建 logout.php文件，

```php
session_start();
session_destroy();
header('Location:login.php');
```



## 小结

会话技术

​	http 协议无连接，无状态，为了弥补这个不足，所以才有会话技术

cookie

​	以 http 协议为基础，服务器端将数据保存在客户端，不重要，有意义的数据(如：id)

​	cookie 保存的数据不是敏感的数据， 例如：密码，用户名...

​	设置 cookie

​		setcookie(name,value,expire，path， domain，secure, httponly);

​			expire 	以时间圆点为起点
​			path		设置cookie的 php 文件在服务器上的路径， 所设置的 cookie 位于浏览器端显示的路径， 如果没有设置 path， 默认这两个路径是一样的， 设置cookie 整站有效

```php
setcookie(name,value,expire, '/');
```

​			domain  设置 cookie 跨域，只能 跨二级域名

​	cookie 删除： 设置过期时间， 将cookie 的值设为空

​		$_COOKIE 用于存储从客户端接收到的 cookie 的数据

session

​	以 cookie 为基础，在服务器端，将重要的数据保存到一个文本文件中，同时将这个文件名以cookie 的形式保存在客户端

session 的主要作用，就是跨脚本共享数据



session_start()

$_SESSION 内存变量

session 文件

我们在代码只需要操作 $_SESSION 内存变量即可，对于数据保存到 session 文件中，或从 session 文件中读取数据，这需要 session 机制自己完成，不需要我们参与

销毁sessoin

全部销毁

session_destroy();

销毁部分

unset($_SESSION['下标'])

cookie session 的区别，