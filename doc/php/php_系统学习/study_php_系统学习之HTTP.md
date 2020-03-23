# study_php_系统学习之HTTP

[TOC]

## HTTP协议

### 1. 概念

超文本协议，http互联网一个基石， 就是客户端与 web 服务器的通讯规则，规定了通讯时所采用的格式，以及格式的含义



### 2. HTTP协议的特点

> 1.  支持 c/s 结构(客户端/服务器)
> 2. 简单，客户端向服务器发起请求时，只需要传递所请求的文件即可
> 3. 灵活，服务器向客户端相应数据，可通过 content-type 来设置返回的数据类型
> 4. 无连接， 服务器只处理一次请求，请求一次就断开连接
> 5. 无状态



### 3. HTTP协议的组成

HTTP协议包含两部分组成

​	由客户端发起的请求部分

​	由服务器端对客户端相应的部分



### 4. HTTP 请求

HTTP的请求时由浏览器根据用户输入的 URL 而自动进行组织的



请求由三部分组成

> 1. 请求头
>    请求的方式 
>    url 请求的文件名
>    协议级版本号	HTTP/1.1
> 2. 报头
>    Host  请求的域名
>    connect  保持连接
>    user-agent  浏览器的相关信息，会自动携带给服务器
>    Accept   浏览器所能处理的数据的格式
>    Accept-Encoding   浏览器所支持的压缩格式
>    Accept-Language    浏览器所支持的语言
>    If-Modified-Since   用于询问当前所请求的内容，自从上次 是否有修改过
> 3. 空行  用于分隔协议头 以及 实际的数据



### 5. HTTP 响应

HTTP协议的响应是由web 服务器根据用户的请求，进行处理后，自动进行组织的

> 1. 响应行 
>    协议及版本号： HTTP/1.1
>    状态码	
>    状态描述
>    常见的状态码：	
>    	200
>
>    ​	404
>    ​	403
>
> 2. 响应报头
>    Date
>    Server   服务器相关的信息
>
>    Last-Modified    与客户端请求头中的Last-Modified-Since 对应
>    Content-type  响应的数据是什么格式，默认都是text/html
>    Content-type   返回数据的长度  318
>    Accenpt-Range： 表示返回的数据值的单位
>
> 3.  空行



### 6. PHP 操作 HTTP 响应头

默认 HTTP 协议 的响应头是由 web 服务器自动组织的，但是 PHP 为我们提供了一个设置 HTTP 响应的协议头的函数 header

> 1. 设置浏览器的显示编码
>    语法：
>    	header('Content-type:text/html;charsett=utf8');
>    说明：
>    	content-type	用于设置相应的数据的格式
>    	charset			用于设置相应的数据中数据的编码
>
> 2. 用于进行跳转
>    语法:
>        header('location:url')
>
>    ```php
>    //下载
>    //1。 通过协议头告诉浏览器，将要发送给你的数据，应该作为一个应用程序数据
>    header('Content-type:application/octet-stream');
>    //2. 通过协议头高数浏览器，将要发送给你的数据，作为附件下载
>    header('Content-disposition:attachment; filename=game.jpg')
>    //3.读取所要发送的文件内容，并发送给客户端
>    $content = file_get_contents('123.jpg');
>    echo $content;
>    ```



## 





