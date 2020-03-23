# study_php_系统学习之数据采集curl

[TOC]

## 什么是数据采集

我们创建网站时为了显示数据，但是有一些数据的获取成本是非常高的，所谓得数据采集就是将别人网站中得数据，为我们所有



## curl 函数介绍 command url

command url

Curl 是一个 代码版的浏览器，允许我们在代码中像使用浏览器一样访问别人的页面

默认php没有 开启对curl 的支持，需要我们要配置文件中手动的开启



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
curl_setopt($ci, CURLOPT_POSTFIELDS,$data);//用于设置post请求所携带的数据

//运行
curl_exec($ci);
```





## curl 函数得使用