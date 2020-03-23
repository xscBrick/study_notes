Study_shell

[TOC]

```shell
#! /bin/sh

# update conntrackd netlink buf
echo "update netlink buffer"
sed -i 's/2097152/256000000/g'  /etc/conntrackd/conntrackd.conf
sed -i 's/8388608/1024000000/g' /etc/conntrackd/conntrackd.conf

# update conntrackd udp socket buffer
echo "update socket buffer"
sed -i 's/1249280/512000000/g' /etc/conntrackd/conntrackd.conf

# update resend queue
if ! cat /etc/conntrackd/conntrackd.conf | grep ResendQueueSize > /dev/null; then
	echo "update resend queueu len"
	sed -i '/DisableExternalCache On/a\ResendQueueSize 2560000' /etc/conntrackd/conntrackd.conf
fi

# restart conntrackd to take effect
echo "restart conntrackd"
/usr/local/vpcgw-ha/conntrackd_stop.sh
while [ -e /var/run/conntrackd.ctl ]; do
	echo "stoping";
	sleep 1;
done
/usr/local/vpcgw-ha/conntrackd_start.sh
while [ ! -e /var/run/conntrackd.ctl ]; do
	echo "starting";
	sleep 1;
done
echo "restart success"
if ip addr show dev uvmac 2>&1 | grep inet > /dev/null; then
	echo "push conntrack to backup"
	sleep 1
	echo "now push"
	/usr/local/sbin/conntrackd -C /etc/conntrackd/conntrackd.conf -B
else
	echo "this is slave, no action."
fi

#check
val=`conntrackd -s runtime | grep 'current buffer size' | awk -F':' '{print $2}' | sed 's/[[:space:]]//g'`
if [ $val'x' == 256000000'x' ]; then
	echo "success"
else
	echo "fail"
fi

```

## /dev/null 位桶 || 黑洞

 在类Unix系统中，/dev/null，或称空设备，是一个特殊的设备文件，它丢弃一切写入其中的数据（但报告写入操作成功），读取它则会立即得到一个EOF。

空设备通常被用于丢弃不需要的输出流，或作为用于输入流的空文件。当你读它的时候，它会提供无限的空字符(NULL, ASCII NUL, 0x00)。

```shell
cat $filename >/dev/null 
#不会得到任何信息，因为我们将本来该通过标准输出显示的文件信息重定向到了 /dev/null 中
cat $filename 1>/dev/null #1->标准输出, 2->标准错误
cat $badname 2>/dev/null #禁止标准错误的输出
```

有些时候，我并不想看道任何输出，我只想看到这条命令运行是不是正常，那么我们可以同时禁止标准输出和标准错误的输出:    

```shell
cat $filename 2>/dev/null >/dev/null
cat $filename &>/dev/null
```

## sed

sed是一个很好的文件处理工具，本身是一个管道命令，主要以行为单位进行处理，可以将数据行进行替换、删除、新增、选取等特定工作。

1. ### sed命令行格式

  ```shell
  sed [选项] [命令]
  ```

### 1.1 选项

-n，使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN 的数据一般都会被列出到终端上。但如果加上 -n 参数后，则只有经过sed特殊处理的那一行(或者动作)才会被列出来。

-e，直接在命令列模式上进行sed的动作编辑。

-f，直接将sed的动作写在一个文件内。-f filename 则可以运行filename内的sed命令。

-r，sed 的动作支持的是延伸型正规表示法的语法。(默认是基础正规表示法语法)

-i，直接修改读取的文件内容，而不是输出到终端。

### 1.2 指定行数

[n1[,n2]]function

n1, n2，不一定存在，一般代表“选择进行动作的行数”，如果我的动作需要在10到20行之间进行，则有’10,20命令’

### 1.3 常用命令

a，新增，a的后面可以接字符串，而这些字符串会在新的一行出现(目前的下一行)

c，取代，c的后面可以接字符串，这些字符串可以取代n1，n2 之间的行

d，删除，因为是删除，所以d后面通常不接任何东西

i，插入，i的后面可以接字符串，而这些字符串会在新的一行出现(目前的上一行)

p，输出，即将某个选择的文件输出。通常p会与参数sed -n 一起使用

s，取代，直接对某些字符串进行替换

- 删除某行

```shell
sed '1d' ab.txt         # 输出删除第一行后的文件内容
sed '$d' ab.txt         # 输出删除最后一行后的文件内容
sed '1, 2d' ab.txt      # 输出删除第一行到第二行后的文件内容
sed '2, $d' ab.txt      # 输出删除第2行到最后1行后的文件内容
```

- 显示某行

```shell
sed -n '1p' ab.txt           # 只显示文件的第一行 
sed -n '$p' ab.txt           # 只显示文件的最后一行
sed -n '1, 2p' ab.txt        # 只显示文件的第一行到第二行
sed -n '2, $p' ab.txt        # 显示文件的第二行到最后一行
```

- 使用安静模式进行查询

```shell
# 输出关键字ruby所在行的内容；其中'/str/p'，str为搜索的文本内容
sed -n '/ruby/p' ab.txt

# 输出关键字$所在行的内容，使用反斜线\屏蔽特殊含义
sed -n '/\$/p' ab.txt
```

- 增加一行或多行字符串

```shell
# 在第一行后增加字符串"drink tea"
sed '1a drink tea' ab.txt     

# 在第一行到第三行后增加字符串"drink tea"
sed '1,3a drink tea' ab.txt   

sed '1a drink tea\nor coffee' ab.txt # 在第一行后增加两行，换行使用\n，可多次使用\n添加多行
```

- 替代一行或多行

```shell
sed '1c Hi' ab.txt    # 把ab.txt的第一行替换为Hi

sed '1,2c Hi' ab.txt  # 把ab.txt的第一行到第二行替换为Hi
```

- 替换一行中的某部分字符串

  格式：`sed 's/要替换的字符串/新的字符串/g' ab.txt`（要替换的字符串可以用正则表达式）

```shell
sed 's/ruby/bird/g' ab.txt   # 把全部的ruby替换为bird

sed 's/ruby//g' ab.txt   # 把全部的ruby替换为空，即删除ruby字符串
```



### 3. sed -i 命令详解

```shell
# 对每行匹配到的第一个字符串进行替换
sed -i 's/原字符串/新字符串/' ab.txt 

# 对全局匹配上的所有字符串进行替换
sed -i 's/原字符串/新字符串/g' ab.txt 

# 删除所有匹配到字符串的行
sed -i '/匹配字符串/d'  ab.txt  

# 特定字符串的行后插入新行
sed -i '/特定字符串/a 新行字符串' ab.txt 

# 特定字符串的行前插入新行
sed -i '/特定字符串/i 新行字符串' ab.txt

# 把匹配行中的某个字符串替换为目标字符串
sed -i '/匹配字符串/s/源字符串/目标字符串/g' ab.txt

# 在文件ab.txt中的末行之后，添加bye
sed -i '$a bye' ab.txt   

# 对于文件第3行，把匹配上的所有字符串进行替换
sed -i '3s/原字符串/新字符串/g' ab.txt 
```

```shell
if ! cat test_shell | grep ResendQueueSize > /dev/null; then
	echo "update resend queueu len"
	sed -i '/DisableExternalCache On/a\ResendQueueSize 2560000' ./test_shell
fi
```

## 文件比较符

文件比较运算符 
-e filename 如果 filename存在，则为真 [ -e /var/log/syslog ] 
-d filename 如果 filename为目录，则为真 [ -d /tmp/mydir ] 
-f filename 如果 filename为常规文件，则为真 [ -f /usr/bin/grep ] 
-L filename 如果 filename为符号链接，则为真 [ -L /usr/bin/grep ] 
-r filename 如果 filename可读，则为真 [ -r /var/log/syslog ] 
-w filename 如果 filename可写，则为真 [ -w /var/mytmp.txt ] 
-x filename 如果 filename可执行，则为真 [ -L /usr/bin/grep ] 
filename1-nt filename2 如果 filename1比 filename2新，则为真 [ /tmp/install/etc/services -nt /etc/services ] 
filename1-ot filename2 如果 filename1比 filename2旧，则为真 [ /boot/bzImage -ot arch/i386/boot/bzImage ] 
字符串比较运算符 （请注意引号的使用，这是防止空格扰乱代码的好方法） 
-z string 如果 string长度为零，则为真 [ -z “myvar”]−nstring如果string长度非零，则为真[−n“myvar”]−nstring如果string长度非零，则为真[−n“myvar” ] 
string1= string2 如果 string1与 string2相同，则为真 [ “myvar”=“onetwothree”]string1!=string2如果string1与string2不同，则为真[“myvar”=“onetwothree”]string1!=string2如果string1与string2不同，则为真[“myvar” != “one two three” ] 
算术比较运算符 
num1-eq num2 等于 [ 3 -eq mynum]num1−nenum2不等于[3−nemynum]num1−nenum2不等于[3−nemynum ] 
num1-lt num2 小于 [ 3 -lt mynum]num1−lenum2小于或等于[3−lemynum]num1−lenum2小于或等于[3−lemynum ] 
num1-gt num2 大于 [ 3 -gt mynum]num1−genum2大于或等于[3−gemynum]num1−genum2大于或等于[3−gemynum 

## No such file or directory

可能是 win 下编辑的 .sh 上传到linux 下导致的

^M
解决方法 : 命令模式下             : set ff=unix

![1569750366555](C:\Users\v_xscxu\AppData\Roaming\Typora\typora-user-images\1569750366555.png)



![1569750329656](C:\Users\v_xscxu\AppData\Roaming\Typora\typora-user-images\1569750329656.png)

set ff ->  fileformat=unix