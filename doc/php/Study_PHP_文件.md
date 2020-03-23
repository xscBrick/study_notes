# Study_PHP_文件

[TOC]

## 文件锁

| 锁类型  | 说明                       |
| ------- | -------------------------- |
| LOCK_SH | 取得共享锁定（读取的程序） |
| LOCK_EX | 取得独占锁定（写入的程序） |
| LOCK_UN | 释放锁定（无论共享或独占） |

```php
$fp = fopen("demo2.txt", "r+");
    
    // 进行排它型锁定
    if (flock($fp, LOCK_EX)) {
    
        echo '1';
    
        fwrite($fp, "文件这个时候被我独占了哟\n");
    
        // 释放锁定
        flock($fp, LOCK_UN);
    } else {
        echo "锁失败，可能有人在操作，这个时候不能将文件上锁";
    }
    
    fclose($fp);
```

### fopen()

fopen() 函数用于在 PHP 中打开文件，此函数的第一个参数含有要打开的文件的名称，第二个参数规定了使用哪种模式来打开文件。

模式 描述

r 只读。在文件的开头开始。
r+ 读/写。在文件的开头开始。
w 只写。打开并清空文件的内容；如果文件不存在，则创建新文件。
w+ 读/写。打开并清空文件的内容；如果文件不存在，则创建新文件。
a 追加。打开并向文件文件的末端进行写操作，如果文件不存在，则创建新文件。
a+ 读/追加。通过向文件末端写内容，来保持文件内容。
x 只写。创建新文件。如果文件以存在，则返回 FALSE。
x+ 读/写。创建新文件。如果文件已存在，则返回 FALSE 和一个错误。

```php
$str="This is a test from www.nowamagic.netn";
//写入文件
$file_pointer = fopen("aa.txt","r+");   
fwrite($file_pointer,$str);
fclose($file_pointer);
//读取文件
$file_name="aa.txt";
$fp=fopen($file_name,'r');
while(!feof($fp)){
    $buffer=fgets($fp,4096);
    $buffer = str_replace("nowamagic","现代魔法",$buffer);
    $buffer = str_replace("This is a test","这是一个实例",$buffer);
    echo $buffer."<br />";
}
fclose($fp);
```

#### feof()

检测 End-of-file

feof() 函数检测是否已达到文件的末端 (EOF)，在循环遍历未知长度的数据时，feof() 函数很有用。注释：在 w 、a 以及 x 模式，您无法读取打开的文件！

## 执行脚本文件  exec()/shell_exec()/system()/passthru()

string exec ( string command [, array &output [, int &return_var]] ) 

string shell_exec ( string cmd)直接执行命令cmd)直接执行命令cm，输出命令执行结果，如果执行过程中发生错误或者进程不产生输出，则返回 NULL，所以，使用本函数无法通过返回值检测进程是否成功执行。

string system ( string command [, int &command [, int &return_var ] ) 

void passthru ( string command [, int &command [, int &return_var ] ) 

### 状态码 exec

如果返回0是运行成功， 
在Bash中，当错误发生在致命信号时，bash会返回128+signal number做为返回值。 
如果找不到命令，将会返回127。 
如果命令找到了，但该命令是不可执行的，将返回126。 
除此以外，Bash本身会返回最後一个指令的返回值。 
若是执行中发生错误，将会返回一个非零的值。 

# 如何在客户端上传shell脚本文件，并利用PHP调用执行脚本

https://blog.csdn.net/guotingting923/article/details/80230371

