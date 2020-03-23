# study_php_apache安装

[TOC]

## 下载apache

[下载地址](http://httpd.apache.org/)如图所示

![image-20191211220202283](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191211220202283.png)

1. 点击[Download](http://httpd.apache.org/download.cgi#apache24)
2. 点击[Files for Microsoft Windows](http://httpd.apache.org/docs/current/platform/windows.html#down)

![image-20191211220404593](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191211220404593.png)

3. 点击[ApacheHaus](http://www.apachehaus.com/cgi-bin/download.plx)

![image-20191211220433443](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191211220433443.png)



点击[Apache 2.4 VC14](https://www.apachehaus.com/cgi-bin/download.plx#APACHE24VC14)

![image-20191211220604301](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191211220604301.png)



选择对应的 系统进行下载

下载apache 到此就结束了



## 安装apache

将下载好的压缩包，解压到指定文件夹

```
C:/software/WAMP/Apache2.4/
```

在C:/software/WAMP/Apache2.4/Apache24/conf/httpd.conf文件修改根文件

```
#Define SRVROOT "/Apache24"
Define SRVROOT "C:/software/WAMP/Apache2.4/Apache24"
```

安装apache

```
httpd -k install
```

报错：

```
httpd.exe -k install -n "Apache2.4
```

启动apache

```
httpd -k start/stop/restart
```



查看是否安装成功

win+r->server(服务)

![image-20191211221243607](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191211221243607.png)

启动

```
httpd -t start 
```

停止

```
httpd -t stop
```

重启

```
httpd -t restart
```

![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605104943358-1041987373.png)

## 三、Apache相关配置------主机配置[#](https://www.cnblogs.com/EricZLin/p/9139059.html#2252064792)

#### 1.httpd.conf------conf目录下[#](https://www.cnblogs.com/EricZLin/p/9139059.html#1684262892)

- SRVROOT安装位置(通过在顶端定义了一个常量，在下面引用该常量来访问，好处不用多说了，之后改动只要改这一个即可，其他的都是相对路径了)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133440706-950611914.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133440706-950611914.png)

- Listen 监听端口号,默认80

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133606266-1492381579.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133606266-1492381579.png)

- ServerAdmin 用于用户设置管理员邮箱（用于客户端的用户联系管理员，现在很少使用）

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133812462-322263658.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133812462-322263658.png)

- *ServerName 域名*

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133914934-1857527337.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605133914934-1857527337.png)

- DocumentRoot用于设置基站点根目录（网站根目录就是存放网站文件的最顶层目录，通过URL中域名后面的第一个斜线对应映射的就是网站根目录）

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605135039258-529347357.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605135039258-529347357.png)

- Directory配置段

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613102929069-1962287918.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613102929069-1962287918.png)

#### 2.hosts文件----位置一般在C:\WINDOWS\system32\drivers\etc[#](https://www.cnblogs.com/EricZLin/p/9139059.html#553002891)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605141040680-1691065577.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605141040680-1691065577.png)

注:127.0.0.1永远代表本地ip

#### 3.httpd.exe-----bin目录下[#](https://www.cnblogs.com/EricZLin/p/9139059.html#1423347345)

- cmd里dir可以查看当前目录的内容,cd可以更改目录的位置
- httpd.exe文件可以进行Apache服务的启动(httpd.exe - k start),停止(httpd.exe - k stop)和重新启动(httpd.exe - k restart)
- httpd.exe文件可以对配置文件进行语法检查(httpd -t)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605142544050-712855833.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605142544050-712855833.png)

注:在win10系统中,需要用管理员的身份运行

#### 4.window环境变量:window的环境变量记录了很多的路径,当在cmd窗口执行一个命令时,如果当前的目录找不到我们要执行的文件时,window会找到环境变量中所记录的位置,依次进行查找,找到了就运行,找不到则报错[#](https://www.cnblogs.com/EricZLin/p/9139059.html#1640722399)

-  .“计算机”右键 → “高级系统设置” → “高级” → “环境变量”

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605143043375-1811463453.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605143043375-1811463453.png)

 

- .点击系统变量的“新建”→ 变量名"HTTPD_HOME" → 变量值“E:\WAMP\Apache2.4”（Apache安装路径）→ “确定”

   注意：变量值后面不能添加分号“;”,否则配置不成功。

- .点击系统变量的“编辑”（没有时新建）→ 变量名"Path" → 变量值“%HTTPD_HOME%\bin;”（Apache的bin目录的路径）→ “确定”

   注意：变量值后面的分号“;”必须是英文分号。path：操作系统提供的环境变量。classpath：程序中引用的类所在的路径。

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605143729127-1698990863.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605143729127-1698990863.png)

- .设置成功后，手动重启cmd，录入命令[ httpd -k restart ]重启Apache服务。若是启动，说明系统环境变量配置成功。

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605144736630-1182551081.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605144736630-1182551081.png)

- 以上所在window7系统里的安装，window10里面安装更加便捷，可以自行百度

## 四、Apache相关配置------虚拟主机配置:使用一个Apache软件配置多个主机(域名)[#](https://www.cnblogs.com/EricZLin/p/9139059.html#2071871820)

#### 1.开启扩展配置文件(默认是关闭的)----httpd.conf[#](https://www.cnblogs.com/EricZLin/p/9139059.html#1822789180)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613115714465-1650320541.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613115714465-1650320541.png)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613115722956-851828834.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613115722956-851828834.png)

#### 2.配置虚拟主机-----httpd-vhosts.conf[#](https://www.cnblogs.com/EricZLin/p/9139059.html#4019694821)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613120026749-420970558.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613120026749-420970558.png)

### 3.注意的问题:[#](https://www.cnblogs.com/EricZLin/p/9139059.html#2849492259)

- 如果是测试需要使用配置的域名的话,需要修改host文件达到目的,原因是这个域名并不是属于自己的,没有办法修改这个域名在公网上的DNS

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613135622137-1485263266.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613135622137-1485263266.png)

- 如果使用了虚拟主机,则默认必须全部使用虚拟主机,即之前的默认网站也必须通过虚拟主机方式配置,否则访问不到,参考文章:[Apache HTTP Server 虚拟主机配置](http://blog.51cto.com/skypegnu1/1532454)
-  Chrome 浏览器 63版本以后，所有的 .dev 和 .app 后缀的网址都将会自动将 HTTP 转到 HTTPS 上，所以如果使用上面的.dev后缀的网址,会出现在Chrome无法访问的情况,但是在其他浏览器可以正常访问,原因就出在这(确实被坑了一道!!!)

### 五、Apache相关配置------外部配置文件[#](https://www.cnblogs.com/EricZLin/p/9139059.html#3048845436)

#### 1.开启外部配置文件httpd.conf中开启**AllowOverride All**[#](https://www.cnblogs.com/EricZLin/p/9139059.html#4057542359)

[![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613134614991-1318032090.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180613134614991-1318032090.png)

#### 2..hatacss文件创建(只能通过编辑器另存的方式来创建)---此文件中的配置不需要重新启动Apache[#](https://www.cnblogs.com/EricZLin/p/9139059.html#4049772640)

#### 3.补充:自定义错误提示页面(ErrorDocument)[#](https://www.cnblogs.com/EricZLin/p/9139059.html#3478482320)

 [![img](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605145741517-1358924990.png)](https://images2018.cnblogs.com/blog/1319779/201806/1319779-20180605145741517-1358924990.png)