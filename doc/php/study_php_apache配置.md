# study_php_apache配置

[TOC]

## htdocs目录：站点根目录(域对应的目录)

## conf/httpd.conf

apache的安装目录

#### SeverRoot

```
 SeverRoot "C:/software/WAMP/apache/Apache24"
```

#### Listen

```
Listen 80
```

多个端口号的设置：

```
Listen 80
Listen 3306
```

#### modules 功能模块

#### ServerAdmin 管理员邮箱

#### DocumentRoot 用于设置文档的根目录/站点根目录

```
 DocumentRoot "C:/software/WAMP/apache/Apache24/htdocs"
```

## Directory 主要用于对站点根目录的特性设置

```
<Directory "C:/software/WAMP/apache/Apache24/htdocs">
	// 1.Directoryindex 用于设置默认首页，当仅指定了域名，没有指定具体的文件时，apache会将此项设置的文件返回给客户
	Directoryindex 
	
	// 2.Options Indexes FollowSymLinks 是否列出目录结构
	 Options Indexes FollowSymLinks
	
	// 3. 用于配置 是否开启外部配置文件 None / All
	AllowOverride None
	
	// 4. order 用于配置此目录的访问权限
	// 4.1 order deny，allow 没有明确的拒绝，全部允许
	order deny，allow
	deny from 110.110.110.110
	allow from all
	// 4.2 order allow，deny 没有明确的允许，全部拒绝
	
	// 5.所有请求都需要认证(授权)
	Require all granted
</Directory>
```



业务场景

域名： www.php9.com

站点根目录 	e:\php9

默认首页： 	index.html

允许列出目录结构

不允许 110.110.110.110 访问

```
ServerName www.php9.com
DoucmentRoot "e:\php9"
<Directory "e:\php9">
	DirectoryIndex index.html
	Options Index FollowSymLinks
	AllowOverride All
	Require all Granted
</Directory>
```

本地域名配置

```
hosts
127.0.0.1      www.php9.com 
```



## 虚拟主机得配置

所谓得虚拟主机就是用使用一个apache 软件，配置多个主机(域名)

### 1. 开启扩展配置文件

默认虚拟主机得配置文件(httpd-vhosts.conf)没有开启

，如果想要配置虚拟主机，需要在著配置文件中开启对扩展配置文件得加载

![image-20200102231546382](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200102231546382.png)

### 2. 在扩展文件中配置多个主机

需求：

```
主机A:
	域名	www.one.com
	站点根目录	d:/one
	默认首页	one.html
	允许列出目录结构
	不允许 110.110.110.110 访问
	
主机B：
	域名	www.two.com
	站点根目录	d:/two
	默认首页	two.html
	允许列出目录结构
	不允许 120.120.120.120 访问
	
```



## 外部配置文件

apache 除了主配置文件 conf/httpdf.conf 与扩展配置文件 conf/extra/httpd-vhosts.conf 之外，还有可以在另一个文件中书写 apache 的配置，这个文件就是 外部配置文件，外部配置文件的默认文件名为 **.htaccess**

### 1. 开启外部配置文件

```
AllowOverride all
```

### 2. .htaccess 文件创建

只能通过编辑器另存的方式来创建这样的文件

### 3. .htaccess 文件的作用

特点：

​	此文件中配置的修改不需要重新 启动apache

自定义错误提示页面

语法： 

```
ErrorDocument 错误代码 \错误显示文件
```

url 重定向

