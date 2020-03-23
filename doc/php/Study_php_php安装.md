# Study_php_php安装

[TOC]

php 就是一个软件包不需要安装，只需要再 Apache 启动的过程中加载 PHP 功能模块即可





将php文件复制到wamp文件夹下

## 2. apache 加载 php

默认 Apache 仅能处理 html 文件的请求，如果想让 Apache 支持 php 文件的请求，必须加载 PHP 这个功能模块

### 2.1 加载php功能模块

httpd.conf

```
#加载php功能模块
LoadModule php7_module C:/software/WAMP/php/php7apache2_4.dll
#配置php文件的扩展名

```

### 2.2  配置php文件的扩展名



### 2.3 加载php的配置文件

php 的配置文件位于php目录中

php.ini-development

php.ini-production 上线阶段的模板文件

```
PHPIniDIR "C:/software/WAMP/php/php.ini"
#不影响php的运行，但会影响部分功能
```



## 测试

创建一个php文件，由于php功能模块必须由apache 的加载，也就是php文件必须通过域名来访问