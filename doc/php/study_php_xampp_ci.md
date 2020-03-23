文章目录
XAMPP的安装及使用教程
1、简介
2、安装运行
3、配置Apache
4、配置MySQL
5、测试
6、修改MySQL默认密码（**此处可不必修改密码，因为有些人修改密码后，后面的操作会出现一些问题，所以最好不要修改了哦**）
7、部署
XAMPP的安装及使用教程
1、简介
XAMPP（Apache+MySQL+PHP+PERL）是一个功能强大的建站集成软件包。这个软件包原来的名字是 LAMPP，但是为了避免误解，最新的几个版本就改名为 XAMPP 了。它可以在Windows、Linux、Solaris、Mac OS X 等多种操作系统下安装使用，支持多语言：英文、简体中文、繁体中文、韩文、俄文、日文等。

许多人通过他们自己的经验认识到安装 Apache 服务器是件不容易的事儿。如果您想添加 MySQL、PHP 和 Perl，那就更难了。XAMPP 是一个易于安装且包含 MySQL、PHP 和 Perl 的 Apache 发行版。XAMPP 的确非常容易安装和使用：只需下载，解压缩，启动即可。

Vista 用户请注意：由于对 Vista 默认安装的 c:\program files($\times$86) 文件夹没有足够的写权限，我们推荐您为 XAMPP 安装创建新的路径，如 c:\xampp 或 c:\myfolder\xampp。

2、安装运行
下载地址：https://www.apachefriends.org/zh_cn/download.html
进入后选择自己对应的操作系统下载（Windows、Linux、Solaris、Mac OS X 等多种操作系统），此处我的系统为Windows操作系统，如果你是其他的操作系统，本教程也可作为参考。

下载后可根据提示一步步进入安装，与安装其他任何软件一样此处不再做出说明，这里我的软件的安装目录为D:\XAMPP，文件夹内容如下图（嘿嘿，因为是猪猪女孩所以懒，这里被我省略了几个哈）：

注意：安装路径，最好放置到D盘，不建议不要放到系统盘去，尤其是早期的XAMPP版本可能默认安装Program files下可能在Vista、Windows 7可能需要修改写入权限。


下面就开始来到我们的初始化与启动环节：
双击运行目录内的setup_xampp.bat初始化xampp。然后运行 xampp-control.exe 可以启动或停止apache、mysql等各个模块并可将其注册为服务。


3、配置Apache

把httpd.conf中的80端口全部修改为8081，如果不修改，会与默认80端口产生冲突，严重时可能导致浏览器不能正常使用。（注意：没有更改Apache的端口时，使用的是 http://localhost 访问xampp主页；更改后， 假设80改为了8081 则使用 http://localhost:8081 访问xampp主页， 访问xampp下的其他php也是这样）



./apache/conf/httpd-ssl.conf文件把端口443修改为4433




4、配置MySQL

把my.ini中的3306改为3316（如果3306不冲突，可以不修改）
把my.ini中的字符集改为utf8，原文档中已有，但需要取消注释（如果不配置utf8，取出的中文是乱码）.

另外，MySQL数据库也需要设置字符集，默认字符集为latin1，在数据库中会造成中文乱码，在创建数据库和数据表时都要注意使用utf8字符集。

点击XAMPP控制面板上的start按钮，启动Apache服务器、MySQL服务器，Apache默认网站目录为…\xampp/htdocs。




5、测试
接下来在浏览器地址栏输入“http://localhost:8081/dashboard/”，若出现如下界面，那么安装就算成功了。


6、修改MySQL默认密码（此处可不必修改密码，因为有些人修改密码后，后面的操作会出现一些问题，所以最好不要修改了哦）
phpMyAdmin操作数据库和通过doc界面连接数据库或是通过mysql客户端界面控制。
按照默认的安装结果，MySQL没有密码，需要设置密码，可以在xampp中启动apache和mysql后，为mysql设置密码。
在浏览器中输入http://localhost:8081/dashboard/，打开本地管理页面.

点击右上角的“phpMyAdmin”，进入数据库管理页面。

打开用户账户，为root用户修改权限

打开修改密码，为root用户设置密码

打开xampp，修改config.inc.php中的数据库密码（[‘password’] = ‘你的密码’）



7、部署
xampp有两种部署方式：
1、复制文件夹到…\xampp\htdocs目录下，如…\xampp\htdocs\test，浏览器中访问localhost/test（注意：文件夹名字htdocs不用输入）。
2、建立虚拟目录
打开xampp，在httpd-xampp.conf文件中建立虚拟目录


经过上述的配置后 xampp 的基本配置已经完成了，请记住您的站点根目录为 xampp 目录下的 htdocs 文件夹。您可以在 htdocs 目录下创建任意一个站点。例如将 test.php 放在 .\xampp\htdocs\new 路径下，您就可以在浏览器的地址栏中输入 http://localhost/new/test.php 来访问这个文件。

下篇我将讲解（图文详细）通过XAMPP导入WordPress网站建立个人博客
如果有需要的话，可以点击进入学习哦（PS: 刚刚安装完成XMAPP的你很有必要继续学习一下XAMPP的实战部分哦！！）

————————————————
版权声明：本文为CSDN博主「Sunny王维」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_36595013/article/details/80373597