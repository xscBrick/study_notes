# study_怎么卸载Apache？

(https://www.php.cn/static/images/article1.png)](https://www.xp.cn/linux.html)![img](https://img.php.cn/upload/article/000/000/024/5d0332b6a1e5c940.jpg)



**卸载Apache的步骤如下：**

1、停止apache服务

按WIN+R打开运行窗口，输入services.msc点击确定。

![9e868dddade23dc345c6c9266623a7e.png](https://img.php.cn/upload/image/959/400/343/1560489741622394.png)

在服务中找到apace服务，点击右键——属性。

![a7039481dde40377ef9c5a8eed461fb.jpg](https://img.php.cn/upload/image/681/438/459/1560489759509468.jpg)

在弹出的设置里将启动类型设为禁用。

![6d41a9cbd2b71231bd83d5f821e7300.png](https://img.php.cn/upload/image/991/156/433/1560489769786034.png)

2、使用cmd命令行程序，删除apache服务

我们再次按WIN+R 然后输入cmd打开命令行。

![048a979e057c1c3bf0ba8c34d998aec.png](https://img.php.cn/upload/image/595/243/572/1560489797259108.png)

输入输入以下命令删除apache服务。

```
sc delete apache
```

![6e9404e9b4fb3945cc7037b8e58c980.png](https://img.php.cn/upload/image/479/829/272/1560489809400681.png)

其他的服务卸载时只需要改动后面的服务名字就可以了。

3、删除apache文件夹

我们找到apache安装的文件夹，这次直接删掉就可以了。这样就解决了卸载Apache服务器的问题了。

![636906ff9f9e166499e7c9f1b0eefe5.png](https://img.php.cn/upload/image/891/255/333/1560489820283092.png)

以上就是怎么卸载Apache？的详细内容，更多请关注php中文网其它相关文章