# study_php_系统学习之二

[TOC]

## php基础语法

### 第一天

#### web基本概念

#### apache安装

##### 安装

##### apache的目录结构

#### 五.主机的配置

##### 1.httpd.conf详解

ServerRoot apache的安装位置

> IP在计算机之间进行通讯，是用于标识电脑
> 端口号是用于标识计算机内的具体的程序

Listen：80  apache 默认端口是80 

ServerAdmin 用于设置管理员邮箱

Servername 域名

```
ServerName php9#配置域名要在hosts改配置域名
#C:\Windows\System32\drivers\etc
#win+r -> drivers ->etv->hosts
```

**DocumentRoot** 用于设置文档根目录(站点根目录)

> DocumentRoot 是与 ServerName  对应的，当外部通过域名来访问 apache 服务器时，apache 会到这个域名对应的documentroot 指定的目录当中去找文件，找到就返回，找不到就报错

**Directory**配置段

主要是用于对站点根目录的特性的设置，配置格式如下

```php
<Directory "${SRVROOT}/htdocs">
    Directoryindex index.html #用于设置默认首页，当仅指定了域名，没有指定具体的文件时，apache会将此项设置的文件返回给用户
    
    Options Indexes FollowSymLinks	#是否列出目录结构，当请求的文件不存在时会将站点的目录结构显示出来
    #在开发阶段，要么允许列出目录结构，要么设置默认首页
    AllowOverride None
    #httpd.conf
    Order deny,allow
    deny from 192.168.120.130 #拒绝192.168.120.130
    allow from all
    #仅拒绝IP地址为：192.168.120.130 的客户端访问
    Require all granted #所有的请求都需要授权
    
</Directory">
```



**Options Indexes FollowSymLinks**

![image-20191213232210176](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191213232210176.png)

**AllowOverride** All 或 none  用于配置是否开启外部配置文件

**Order** 配置项 用于配置此目录的访问权限

Order deny，allow  如果没有明确的拒绝则全部允许

```conf
#httpd.conf
Order deny,allow
deny from 192.168.120.130 #拒绝192.168.120.130
allow from all
#仅拒绝IP地址为：192.168.120.130 的客户端访问
```

Order allow,deny	如果没有明确的允许，则全部拒绝 

www.xscphp.com == 127.0.0.1

##### 2.主机的配置zhao'da

##### 3.httpd.exe的作用

###### apache 服务器的维护

管理员登录cmd

httpd.exe -k start/stop/restart 	启动 apache

httpd -t	#t-->test

###### 配置文件的语法检查 httpd -t

###### windows 环境变量

##### 4.虚拟主机的配置

所谓的虚拟主机就是使用一个apache 软件，配置多个主机（域名）

conf/extra/httpd-vhosts.conf

1.开启 httpd.conf

默认虚拟主机的配置文件是没有开启的，如果想要配置虚拟主机，需要在主配置文件中，开启对扩展文件的加载

```
#virtual hosts
Include conf/extra/httpd-hosts.conf //Include加载
```

2.在扩展配置文件中，开启多个主机（虚拟主机）

```
需求：
    主机A:
    域名 	www.one.com
    站点根目录  d:\one
    默认首页 one.html
    允许列出目录结构
    不允许 110.100.110.110访问

    主机B:
    域名 	www.two.com
    站点根目录  d:\two
    默认首页 two.html
    允许列出目录结构
    不允许 120.120.120.120访问

```



##### 5.外部配置文件 .htacess

httpd-vhosts.conf

```
<VirtualHost *:80>
    DocumentRoot "C:/software/WAMP/Apache2.4/Apache24/xscphp"
    ServerName www.xscphp.com:80
    <Directory 'C:/software/WAMP/Apache2.4/Apache24/xscphp'>
        DirectoryIndex index.html
        Options Indexes FollowSymLinks
        #开启外部配置文件
        AllowOverride all
        Require all granted
    </Directory>
</VirtualHost>
```

xscphp-->.htaccess

作用：此文件中配置的修改，不需要重新启动apache

自定义错误提示页面

```
ErrorDocument 错误提示文件
ErrorDocument 404 /error/404error.html
```

/error/404error.html

```
<img src="/error/404.jpg">
```

![image-20191215132441569](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191215132441569.png)



## mysql

安装，custom,browser(浏览-wamp-mysql)，

配置：Launch the mysql Instance Configuration Wizard(开启向导配置)

Detailed Configuration(细节配置，详细配置)

Developer Machin(开发者机器，mysql服务器+)

服务器用法：Multfunctional Database 多功能服务器，Transactional Database Only事务服务器，Non-Transactional Database Only非事务服务器

Enable strict Mode  开启mysql的严格模式

设置存储字符集：Manusal Selected Default Character Set / collation --utf8

注册服务：Install As Windows Service

Include Bin Directory in Windows PATH 设置bin目录环境变量

Modify Securiity Settings 设置密码(root用户)

应用配置 -- Execute

## 安装2

将文件解压到：C:\software\WAMP\mysql
在文件：C:\software\WAMP\mysql 下新建my.ini 配置文件

```
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port = 3306
# 设置mysql的安装目录
; basedir=C:\\web\\mysql-8.0.11
basedir=C:\\software\\WAMP\\mysql
# 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错

# datadir=C:\\web\\sqldata
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

以管理员身份打开cmd 命令

切换到目录：C:\software\WAMP\mysql\bin

初始化数据库：

```
mysql --initialize --console
```

如果data文件夹下有文件会报错，需要先删除data文件夹下的所有文件，再重新初始化数据库

![image-20191215151205573](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191215151205573.png)

随机生成的密码：nqDw+nMTg8vf

![image-20191215151433164](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191215151433164.png)

安装mysql

```
mysqld install
```

启动mysql服务器

```
net start mysql
```

注意: 在 5.7 需要初始化 data 目录：

```
cd C:\software\WAMP\mysql\bin
mysqld --initialize-insecure 
```

初始化后再运行 net start mysql 即可启动 mysql。

#### 测试登录mysql

```
mysql -uroot -pnqDw+nMTg8vf
```

修改密码：

可以用以下指令修改你密码为 root。

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root' PASSWORD EXPIRE NEVER;
```

之后使用以下指令刷新权限：

```
flush privileges;
```

## php的安装

### 下载php

[下载地址](https://windows.php.net/download/)

**如果是使用Apache，必须使用PHP的线程安全（TS）版本**，即：Thread Safe

VC15指的是php需要的运行库，因为php是c/c++语言写的，也需要VC15的支持

![image-20191215162727677](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191215162727677.png)

下载的是压缩包，解压之后的文件夹，自己找个路径放着：C:\software\WAMP\php

### 1.部署

php就是一个软件包，不需要安装，只需要再apache 启动的过程中来加载php功能模块即可

将php文件解压到：C:\software\WAMP\php文件夹

![image-20191215155812389](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191215155812389.png)

### 2. apache 加载 php

默认apache 仅能处理html文件的请求，如果想让apache支持php 文件的请求，必须加载php这个功能模块

**如果是使用Apache，必须使用PHP的线程安全（TS）版本**，即：Thread Safe

#### 1.加载php功能模块

httpd.conf

```
# 加载php  php7apache2_4.dll
LoadModule php7_module 'C:/software/WAMP/php/php7apache2_4.dll'
```

#### 2.设置php文件的扩展名

```
#配置Php文件的扩A展名
AddType Application/x-httpd-php .php
```

 ache分配工作给php模块：如果是php代码就交给php模块处理（通过文件后缀名`.php`判断）
AddType Application/x-httpd-php .php

#### 3.加载 php 的配置文件

文件位于 php 目录中：C:\software\WAMP\php

```
php.ini-development 	开发阶段的配置文件的模板文件
php.ini-production	上线阶段的配置文件的模板文件
```



```
将 php.ini-development 复制一份并更改为 php.ini 即可
php.ini 配置文件的设置，并不影响php的运行,但是会影响php的一些扩展功能
```



```
#设置php 的配置文件 httpd.conf
PHPIniDIR "C:/software/WAMP/php/php.ini"
```

### 测试：

创建一个 php 文件，由于php文件必须由 apache 来加载

也就是php文件的运行必须通过域名来运行，而且不能包含中文

如果php加载了某个功能模块没有生效，可以到



## php时间问题

php.ini

date.timezone = PRC



# php基本语法

快速创建表单

```
table>thead>tr>th*4^^tbody>(tr>td*4)*3
```

php 中变量名必须区分大小写，其余的函数，方法名，类名都不区分大小写，但建议区分

### php标记

标准格式：xml格式

```
<?php ... ?>
```

script 格式

```
<script language="php">
	echo date('Y-m-d H:i:s');
</script>
```



短格式：<? ... ?>

php.ini

```
short_open_tag = On//开启短格式标签
asp_tags = On//开启asp格式的标签
```

asp 格式 <% ... %>

对于短格式，asp格式，需要在php.ini 中开启

#### 变量

内存中用于临死存储数据的一个空间，这个控件有一个名字，这个名字就是变量名，变量名是用于对这个内存中的数据进行引用的

##### 删除变量

删除变量就是从内存中销毁

```
$v =1;
unset($v);
```

##### 可变变量

1. 通过一个变量访问另一个变量

```php
$v = 'age';
$age = 20 ;
echo $v,'<br/>';
echo $$v, '<br/>'
```

2. 通过一个变量创建另一个变量

```php
$v = 'age';
$$v = 20;
```

##### 预定义变量

PHP为我们预先定义了一组变量，这些变量会在不同的需求中使用

```php
$_GET	//用于前台表单使用 get 方式提交的数据
$_POST	//用于接收前台表单使用 post 方式提交的数据
$_REQUSET	//用于接收前台表单使用 get||post 方式提交的数据
$_SERVER	//记录了服务器端与客户端的相关信息
$_COOKIE	//一种会话技术
$_SESSION	//一种会话技术
$_FILES	//用于记录用户上传的文件信息
$GLOBAL	//用于记录全局变量
```

##### $_server

#### ![image-20200108224251981](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200108224251981.png)

### 内存原理

程序语言就是对内存进行操作的

#### 1. 内存结构

##### 1. 栈区

保存的时变量名(术语称之为引用)

ps: $v

特点：对于cpu来说，读写速度时最快的

##### 2. 堆区

存储的是"复杂"的数据：数组，对象, 字符串

##### 3. 数据段

存储的是简单的数据，例如：整型，浮点型，布尔值

3.1数据段全局区

3.2数据段静态区

储存静态变量和常量

##### 4. 代码段

存储的是源代码对应的机器指令，人能看懂的，计算机时看不懂的，必须经过转换

##### 5. 输出缓存

只要遇到输出命令，例如echo，print，print_r,var_dump,这些指令都会将输出内容存储在输出缓存中

#### 2. php 的执行过程

##### 1. 编译阶段

进行语法检查，词法检查，代码优化

编译之后将源代码转换为机器指令

Parse error //编译错误

##### 2. 执行阶段

如果编译通过后，会将源代码对应的机器指令，保存在代码段，再开始执行代码段中的机器指令

![image-20200108231315554](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200108231315554.png)



#### 3. php 嵌入到HTML的执行过程

当php功能模块在处理一个php文件时，它只关心php代码(使用php标签包含的代码)，对于非php 代码，它会原样输出

js，html，css 对于php 来说都是字符串



#### 4. php 中变量的传值方式

##### 1.  赋值传值

使用一个变量为另一个变量赋值时，传递的是变量的值

```php
$v=10;
```



##### 2. 引用传值

```php
$v=10;
$v2 = &$v;//将$v 的物理地址给 $v2
$v2=20;
echo $v1;	//20
```

提示：

js中不允许人为的更改传值方式，但是php中可以使用地址符'&'，来将赋值传改为引用传值(不能将引用传值改为赋值传值)



#### 5. 常量

##### 5.1  概念

常量就是一种特殊的变量，也是用于存储数据，常量一旦定义就不允许修改其值，常量本身也不允许删除

##### 5.2 定义

###### 5.2.1 语法1

```php
define('常量名','常量值');
define('PI', 3.1415);
echo PI;
```

###### 5.2.2 语法2

```php
const '常量名'='值';
```

###### 2.3 define vs const

define 语法可以在分支结构中定义常量，const 不允许

define 定义的常量可以自定是否区分大小写

```php
define('PI',3.14, true);
echo pi;
```

说明：

​	常量一旦被定义就不能修改
​	常量不能被删除
​	常量的值只能是基本数据类型(标量数据类型)
​	常量默认是区分大小写的，一般常量在命名时，用全大写

##### 5.3 常量的判断及获取所有的常量

###### 5.3.1  defined();

判断常量是否存在

```php
$result = defined('PI');
var_dump($result);//bool('false')
```

```php
// 获取php常量函数
$return = get_defined_constants();
echo '<pre>';//格式化输出
print_r($return);
```

###### 5.3.2 get_defined_constants();

![image-20200109010337999](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200109010337999.png)



#####  5.4  魔术常量

```php
__FILE__	//用于获取当前文件的路径和文件名
__DIR__		//用于获取当前文件的路径
__LINE__	//行
__FUNCTION__	//用于获取当前函数的函数名
__METHOD__	//用于获取当前方法的方法名
__CLASS__	//用于获取当前类的类名
__NAMESPACE__//用于获取当前空间的空间名
```

https://8000.tencent.com/wifi/

#### 6. 数据类型的分类

三大类，八小类

##### 6.1 标量(scalar)数据类型

##### int

##### float

##### boolean

###### string

使用单引号定义的字符串

​	能够被转义的字符有 

```
 \\   \'
```

​	单引号定义的字符串中变量不能解析其值

使用双引号定义的字符串

​	能够被转义的字符有  

```php
\"   //双引号
\t	//制表符
\r  //回车符
\n  //换行符
\$ 	//$
\\	//\
```

​	双引号定义的字符串变量的值可以直接解析

```php
$age = 10;
$v = "abcdes$age"; //abcdes10
```



```php
$v1 = 'a,b,c\' bvvns\t'; //,b,c\' bvvns\t
$v2 = "a,b,c\" bvvns\t"; //a,b,c\" bvvns
```

转义符： \
转义符作用：
	用于将程序语言所赋予的某些字符的特殊功能转义掉
	输出 不可见的字符

heredoc

​	也是使用定义字符串，主要用用场景是定义大段的字符串

​	语法：

```php
$str = <<<abc  //开始标记
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<?php 
$return = get_defined_constants();
echo '<pre>';//格式化输出
print_r($return);
?>

</body>
</html>
abc;//结束标记，结束标记必须顶格写，开始标记与结束标记必须相同
```



##### 6.2 复合数据类型

##### array

1.索引数组

​	下标是数字

2.关联数组

​	下标是字符串

**注意：**

​	如果在一个字符串中想输出数组的元素，那么下标不需加引号，如果用{}来限制了数组，那么下标必须加引号

```php
echo '<pre>';
echo $_SEVER['REMOTE_ADDR'];
$h2 = '<h3>$_SEVER[REMOTE_ADDR]</h3>';
$h2 = "<h3>$_SEVER[REMOTE_ADDR]</h3>";
$h2 = "<h3>{$_SEVER['REMOTE_ADDR']}</h3>";
```



##### object

##### 6.3 特殊数据类型

##### null

##### resource 资源类型

资源数据类型也是一个特殊的变量，程序员没有办法直接定义一个资源

必须使用PHP提供的获取资源的函数

```php
$file = fopen('data.txt','r');//获取资源的函数
var_dump($file);
echo fgets($file);
```

### 7. 数据类型的判断

##### 7.1 数据会自动转换

数据用于运算，当参与运算的两个数据，类型不同时，php会自动进行转换，有时也会进行强制转换

```php
$i = 100;
$j = '100元'；
echo $i * $j;	//10000
```

##### 7.2 强制转换

(integer)$i

(string)

(float)

(array)

(object)

(boolean)

##### 7.3 数据及类型的判断

判断函数的格式规律

is_int(v);

is_string();

is_bool();

is_null();



isset(v) 用于判断变量是否有设置值

```
$v = null;
isset = isset($v)//false

```

empty(v)

#### 自操作运算符 ++ / --

##### 自增运算符

前自增 规则 ：先对变量的值自增1，再使用变量的新值参与式子的运算

```php
$i = 10;
$result = ++$v;
echo $v, '<br/>';  //11
echo $result; //11
```

后自增规则：先使用的原值参与式子的运算，再对变量的值进行加1

```php
$i = 10;
$result = $v++;
echo $v, '<br/>';  //10
echo $result; //11
```



```php
$v = 10;
		//11  	11		12	  13	14
$result = $v + ++$v + ++$v + ++$v + ++$v;
echo $result, '<br/>'; //61
echo $v;	//14
```

前加加是先改内存中变量的值，再将新值读取到式子中

后++是先读取内存中的这个变量的值，放在式子中，再对变量的值加1

##### 自减

其他

```php
+=	//$+=2  ==   $ = $i+2
-=	//$-=2  ==   $ = $i-2
*=	//$*=2  ==   $ = $i*2
/=	//$/=2  ==   $ = $i/2
%=	//$%=2  ==   $ = $i%2
.=	//对字符串进行拼接
```



##### 赋值运算

将赋值号右边的值赋值给左边的变量，左边必须是变量，不能是式子



##### 逻辑与 短路

根据逻辑与的假值运算规则，由于第一个操作数$v 的值是false，最终结果就为false, 没有必要再计算第二个式子了，所以 ++$n 并没有得到运行，形象称之为 逻辑与短路

```php
$v = false;
$n = 10;
$result = $v && ++$n;
var_dump($n); //10
```



##### 逻辑或短路

```php
$v = true;
$n = 10;
$result = $v || ++$n;
var_dump($n); //10
```

&&  and

运算符规则与&& 运算规则相同，唯一区别是 &&的优先级高于=， 而and优先级低于=；

||  or

运算符优先级：单，算，关，逻，条，赋，逗

##### 错误抑制符 @

错误信息不会显示

##### 脚本级的错误控制

脚本级的错误控制仅限于当前的php脚本文件

ini_set() 	主要用于在 php 脚本中来设置 php.ini 中的配置项

语法：

​	ini_set(配置项名，值)；

```php
ini_set('display_errors', 'Off');
$link = mysqli_connect('127.0.0.1','root','123');

```



ini_get();

##### 进制转换函数

dec	decimal

bin	binary

oct	octet

hex 	hex

decbin()	十进制转为二进制

```php
$v = 255;
echo decbin($v);
```

dechex() 	十进制转为十六进制

decoct()

## php 的输出语法

print()：	只能输出标量数据类型，对于任何数据都要转换为字符串输出

echo()	: 只输出标量数据类型，对于任何数据要转换为字符串输出

​	echo与print的区别： echo 没有返回值，print有返回值

print_r()：		可以输出数组，但是布尔值还是需要转换

var_dump()：	主要用于代码调试，可以输出十分详细的信息，并不是输出信息给用户

sprintf()：	用于格式化输出，

sprintf(格式化字符串，变量1，变量2...):

格式化占位符有
%b, %d, %o, %x,%f，%s

```php
$v = 255;
echo sprintf('二进制为：%b,<br/> 十进制为：%d,<br/>' ,%v,%v);
```



## php.exe 文件

cmd下

php.exe -S localhost:8000



php_cli

php 的命令行模式

php 01operand.php

php --ini

查看php配置文件



php --help

php -f  文件名/01operand.php

php -r "一行php命令/echo 123;"



# 流程控制

计算机中的流程控制可分为三种

1.顺序结构

2.分支结构

3.循环



### switch结构

当一个问题需要判断的条件比较多时，php又提供了一个switch 分支结构

语法：

```php
switch(变量){
	case 值1：
        语句体1
        break；
   case 值2：
        语句体2
        break；
}
```

 说明：

​	根据switch后的变量与case 后的值匹配的情况，将程序转向不同的与具体执行，break可以省略

当一个语句体执行结束后，如果没有遇到break，则会执行气候的语句体，不会判断其后的case

```php
switch($day){
    case 1:
        echo '星期一';
        break;
    case 2:
        echo '星期二';
        break;
	case 3:
        echo '星期三';
        break;
    default:
        echo '数据不全';
        break;
}
```

if 与 switch的区别

​	if 结构的条件可以表示一个范围，

​	switch 结构的条件主要是表示一个具体的值

### for

for(循环控制变量初始化；表达式；循环控制变量的更改){

​	//循环体

}

### do...while

语法：

```
do{
	//循环体
	
}while(表达式);

```

首先执行循环体， 循环体执行结束后，判断表达式是否成立， 如果不成立，直接结束循环结构

### 循环的结束与退出

#### contnue

语法：continue [n];

说明：

​	n的取值是一个整数，如果省略，默认是1

​	n主要是用在循环嵌套的情况下

​	结束当前循环结构的本次循环，继续上n层循环结构 (用于循环嵌套) 的下一次循环



## php标签语法

### for

将一个for语法结构，放在两个php标签中

```
<?php for($i=0;$i<4;$i++){ ?>
	<tr>
		<?php for($j=0;$j<4;$j++){
			<td><?php echo $data[$i][$j] ?></td>
		<?php } ?>
	</tr>
<?php } ?>
```

```php
//标准语法
<?php for($i=0;$i<4;$i++){ ?>
<?php } ?>

//简化语法
<?php for($i=0;$i<4;$i++): ?>
<?php endfor ?>
```

#### if 

#### while

## 文件引用

在实际开发过程中，经常会在一个php文件中引入其他的文件

被引入的文件可以是 html 也可以是 php 文件

语法

### require

require(文件名)

require_once(文件名)



### include

include(文件名)

include_once(文件名)



文件引用，先引用，后调用

![image-20200115231609876](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200115231609876.png)



### 引入的路径问题

在实际项目中，对于html文件，是不允许用户直接请求，而是指向一个php文件，让php文件来引用这个html文件

当一个 php文件引入一个 html 文档时， html 文件本身也会引入一些其他文件，如：图片文件，css，js



引用相对路径

![image-20200116003310028](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200116003310028.png)



html文件是在浏览器上解读的，php代码是在apache服务器上解读的

include 语法本身可以使用绝对路径

```
include 'e:/C:\software\phpstudy\phpstudy_pro\WWW';
```

### include 与 require 区别

include 在引入文件时，如果被引入文件不存在则会报错，但程序会继续向下执行

require 在引入文件时，如果被引入的文件不存在，则会终端程序的执行

#### 经验法则

require 一般用于引入php文件，因为php里面一般书写的时功能性的代码

include 一般用于引入html文档



### DIR && FILe

```
__DIR__  用于获取文件所在的完整文件名
__FILE__	用于获取文件所在的路径
__FILE__ __DIR__ 并不会被随着被引入后的文件所更改，永远记住文件名与文件夹
```

 

## php中的错误处理机制

### 编译错误

在编译的过程中发生的错误，多是由于书写错误

### 执行错误

在编译通过后，在执行阶段发生的错误

### 逻辑错误

逻辑不严谨导致的，执行结果与预期不符



### 错误代码

在php的错误处理机制中，每一种错误都使用一个错误标识

```
echo '<pre>';
print_r(get_defined_constants());
```

#### 系统错误

E_ERROR 	致命错误
E_WRRING  警告错误，不中断
E_NOTICE	提示错误，不中断
E_PARSE 	编译错误，不中断

### 错误日志控制

error.log

```
error_reporting
```

```php
<?php

ini_set('error_reporting', E_ALL);//显示所有错误
ini_set('error_reporting', E_NOTICE | E_WARING);
```

E_USER_ERROR  致命错误

E_USER_WRRING 警告错误，不中断

E_USER_NOTICE  提示错误，不中断

是否记录错误

log_errors=on/off	

错误日志的位置

如果没有设置， error_log 默认时记录到apache 的错误日志中 \logs\error.log

;error_log = syslog	//记录到错做系统的日志中

系统日志  eventvwr.msc



## 函数

函数名不区分大小写



### 函数的调用 & 可变函数$f()

```
def function nxn(){
	echo n*n;
}
def function showInfo(){
	echo __FUNCTION__;
}
showInfo();

$f = 'showInfo';
$f();

$f = $_GET['f'];
$f();
```



```php
<?php 
echo '<pre>';
prinr_r($_GET);

//www.php8.com/index.php?f=showInfo&name=showName
/*
*array(
f = showInfo,
name = showName
)
*/
```



### 匿名函数 function(){}；

匿名函数是一个闭包(closure)

如果是匿名函数，必须使用分号结尾

```
function(){
	echo __FUNCTION__;
};
```

提示：

​	js中的匿名函数可以自调用，但php中的函数没有办法自调用

​	php 中的匿名函数，可以赋值给一个变量，还可以用与某个函数的参数(可以参数传递个某个函数，形参)

ps:将一个匿名函数作为参数赋值给一个变量

```
$fn = function(){
	echo __FUNCTION__;
};
$fn();
```



#### 回调函数 callback

匿名函数作为回调函数(参数)传递

```php
function showInfo($cb){
	$cb();
}
showInfo(
	function(){
		echo 'hello';
	};
);
```

实参与形参之间也是一种赋值方式

在形参前加 & 改变为引用传值

```php
function myMath($a, &$b){
    $a = 100;
    $b = 200;
    echo $a, '<br/>', $b, '<br/>';//100,200
};
$a = 10;
$b = 20;
myMath($a, $b);
echo $a, '<br/>', $b;//10,200
```



### 伪类型 (函数)

php语言本身提供了 8 中数据类型，但是在使用手册中我么会遇到另外几种

mixed 	表示类型不确定

callback	表示函数

scalar	如果是 int， float， string, bool, 



### 相关函数 系统函数

func_get_args();	用于获取实参，并于数组的形式返回

func_get_arg();	用于获取 ind 下标 func_get_arg(0/1/2/3);

func_num_args();	用于获取实参的个数

```php
function getSum(...$args){
  echo '<pre>';
  print_r($args);
};

function getSum(...$args){
    $sum = 0;
    for($i=0;$i<count($args);$i++){
        $sun += $args[$i];
    }
    echo $sum
};
$getSum(10,20,30,40);
```

说明：

​	...$变量名		用于将实参以数组的元素的形式保存在这个变量中



#### 作用域

函数内部不能访问全局变量

默认 php 中有很'清晰' 的作用域

#### global 关键字

global 变量名；

> 在函数内部，建立一个与函数外部同名的变量的引用， 如果外部没有这样的同名变量，会在外部创建一个同名的变量



```php
$i =10;
function test(){
    global $i;
    $i += 10;
    echo $i;//20
}
test();
echo $i; //20
```



##### $GLOBLAS 预定义变量

```php
$name = 'zhangsan';
$age = 20;
echo '<pre>';
print_r($GLOBLAS);
```



![image-20200118121754023](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200118121754023.png)



#### 静态变量

![image-20200119225743367](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200119225743367.png)

![image-20200119225925165](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200119225925165.png)

##### 原理

静态变量在函数多次呗调用时，只会被初始化一次，并且静态变量的值并不会随着函数执行后空间的销毁而被销毁

在函数下一次被调用时，仍然可以访问其值

##### 编译过程

> 1.编译
>
> 1.1 在编译时发现函数内部有static 声明的变量，会在数据段的静态区存储这个数据，编译通过后会在代码段产生机器指令，会将函数与静态变量进行关联
>
> 2.执行
>
> 2.1 首次执行，会在栈区开辟一个专属于函数本次执行的控件，在函数内部空间内创建变量$i , 将与函数关联的静态变量的地址传递给战区中
>
> 2.2  执行$i++, 根据$i的地址找到静态区中的数据，并加+1
>
> 2.3 echo $i,将数据输出
>
> 2.4 函数执行结束，战区中的函数的空间被销毁
>
> 3.执行 弟2次函数的调用
>
> 3.1 会在栈区开辟一个专属于函数本次执行的空间，
>
> 在函数空间内船舰变量$i, 将与函数关联的静态变量的地址传递给栈区中的，由于$i 有static 修饰，所以$i=1这步不会被执行

##### 静态变量的使用场景

如果想在同一个函数多次调用时，共享一份数据，那么就使用静态变量

## 系统函数

### 日期时间函数

#### 1. time() 时间戳

用于获取当前时间的时间戳，单位是秒，时间戳就是从时间原点至现在的一个秒数(1970.01.01 0:0:0)

#### microtime() 毫秒

#### date() 格式化时间信息

语法：

​	date(string $format[, int $timestamp]);

说明：

​	用于格式化时间信息

​	$format 用于格式化时间的字符串

​	$timestamp 表示所要格式化的时间戳，如果省略表示对当前时间进行格式化。

> Y	年
> m	月
> d	日
> H	小时/24小时制
> i	分钟
> s	秒

#### mktime()

语法：
mktime(时, 分, 秒, 月, 日, 年);

用于获取指定时间的一个时间戳



#### strtotime()

将一个以字符描述的形式的时间转化为时间戳

```
echo time(), '<br/>'; 
echo strtotime('+3 month'), '<br/>'; 
echo strtotime('10 September 2000'), '<br/>'; 
echo strtotime('+1 day'), '<br/>'; 
echo strtotime('+1 week'), '<br/>'; 
echo strtotime('+1 week 2 days 4 hours 2 seconds'), '<br/>'; 
echo strtotime('next Thursday'), '<br/>'; 
echo strtotime('last Monday'), '<br/>'; 
```

### 递归 自己调用自己

```
<?php
// 1 2 3 5 8 13 21 34 55 .....
function func($para){
    return $para < 3 ? $para : func($para - 1) + func($para - 2);
}
echo func(11);
```



## 字符串 常用函数

使用单引号或者双引号括起来的0个或者多个字符

```php
//单引号：
//	不能解析变量的值，能够被转义的 '\\' '\'
$str = "assdfdjkfhaaaasdfdss";
//双引号：
//	能够解析变量的值，都能被转义

//heredoc	本质是使用双引号定义大段的文本，只是以另一种方式进行书写
$heredoc = <<<abc
	assdfdjkfh"aaaasdfdss"
abc;
//nowdoc 	本质是使用单引号定义的大段的文本，只是以另一种方式进行书写
$nowdoc = <<<'abc'
	assdfdjkfh"aaaasdfdss"
abc;
//字符串也可以当作一个有多个字符组成的序列
//示例
$str = "adfjadshf";
echo '$str的第一个字符元素为：'.$str[0], '<br/>'; //$str的第一个字符元素为：a
```



### 字符串长度

#### strlen() 用于获取一个字符串的字节数长度



#### 多字节字符的支持

默认字母再任何字符中占据1个字节保存一个字符

但例如汉字，一个字符可能占据多个字节，所以 php 提供和了对多自己字符的支持

需要在 php.ini 中开启多字节字符的支持

```
extension=php_mbstring.dll
```

开启多字节字符的支持后，我们就可以用多字符的操作函数

mb_string(变量，存储编码)

```php
$str = '你好a';
echo mb_string($str, 'utf-8'), '<br/>';//3
echo strlen($str), '<br/>';//7
```



#### 查找并截取函数

strstr(str,substr);

说明：

​	用于在字符串 str 中，查询子字符串 substr首次出现的位置，并截取到最后



strrchr(str,substr);

说明：

​	用于在字符串 str 中，查询子字符串 substr最后出现的位置，并截取到最后

```php
$str = 'https://www.php8.com/test.php';
$first = strstr($str,'/'); // //www.php8.com/test.php
$last = strrchr($str, '/'); // /test.php 
```



#### 查找

strpos($str, $substr);
strrpos($str, $substr);



#### 分割

explode(分隔符,str)

说明：

​	指定的分隔符，将字符串str 进行分割，返回的是数组；

#### 替换

str_replace(rep,search,str);

在符串str中，查找search 表示的部分，并替换成rep返回





## 数组

### 1. 概念

数组是一种数据的集合

数组主要是用于存储具有行列特征(表格)的数据



### 2. PHP 数组的分类

#### 2.1 索引数组

​	数组的下标是整数

#### 2.2 关联数组

​	数组的下标是字符串

#### 2.3 PHP数组的创建

##### 2.3.1 索引数组的创建

显示创建

```php
$arr = array(10,20);
$arr = [10,20];
```

隐式创建

```php
$arr = array();
$arr[0]=10;
```



##### 2.3.2 关联数组的创建



### 3. 数组的指针

```php
current($arr);	//用于获取当前指针的元素
key($arr);		//当前数组元素的键名
next($arr);		//
prev($arr);
reset($arr);
end($arr);
```

foreach 是通过指针遍历数组

首先对数组的指针进行重置



while-each-list 遍历

使用 while 循环, 及 each()函数，list 语法结构联合来遍历数组

each(); 	用于获取当前指针所指向的元素键名与键值

 

```php
while(true){
	list($k,$v) = each($arr);
	if(!$k){
	break;
	}
	echo $k, '=>', $v, '<br/>';
}

while(list($k,$v) = each($arr);){
    echo $k, '=>', $v, '<br/>';
}
```



### 4. 数组常用函数

#### 数组长度 count()

#### 键值，键名

arrary_keys();

array_values();

#### 判断键名与键值是否存在

array_key_exists();

用于判断某个键名是否在数组中



in_array();

#### 数组排序

sort()

rsort() //索引改变



asort() //索引不变

arsort()  



## 冒泡排序  bubble

```php
$arr = [30,19,39,20,10,15];
$len = count($arr);

//外层循环控制轮数
for($i=0; $i<$len-1; $i++){
    //内层循环控制比较并调换位置
    for($j=0; $j<$len-$i-1; $j++){
        if($arr[$j] > $arr[$j+1]){
            $tmp = $arr[$j];
            $arr[$j] = $arr[$j+1];
            $arr[$j+1] = $tmp;
        }
    }
}
print_r($arr);
```



# 核心编程

## 会话技术

由于http协议是无连接，无状态的，所以http 协议 无法记住客户端的信息

为了弥补这两点的"不足"，所以出现了会话技术

### 一 cookie 技术







# 面向对象



## PDO



## smart



## MVC和blog项目

