# study_php_系统学习之文件

[TOC]

对文件
fopen(filename, r/w/a)	返回一个资源类型 stream

fgetc,  fgets,  fread,  file_get_contents

readfile, file

fwrite()

对目录

opendir()	返回一个资源类型

遍历文件夹

```php
<?php
    
$dir = '';
function gettree($dir){
    $arr = scandir($dir);//把文件读为数组去遍历
}
```



## 1. 文件操作

php 也提供了一套文件操作系统函数。通过这套函数进行文件管理，创建文件，删除，改名，存储数据，读取数据



### 1.1 文件相关信息

1. file_exists //判断文件是否存在



```php
<?php
$file = 'e:/php9/test.php';
$return = file_exists($file); //true || false
```



2. filemtimes();

获取文件修改时间

```php
<?php
$file = 'e:/php9/test.php';
$time = filemtimes($file); 
echo date('H:i:s Y-m-d',$time);
```



3. filesize();

获取文件大小，字节

```php
<?php
$file = 'e:/php9/test.php';
$size = filesize($file); //文件大小
```



4. basename(path);

用于获取文件名

```php
$path = 'c:/php9/2020/hello.txt';
echo '<pre>';
print_r(pathinfo($path));/***
*array(
[diname]=>c:/php9/2020/hello.txt
[basename]=>hello.txt
[extension]=>txt
[filename]=>hello
)
*/

print_r(basename($path));//hello.txt
```

5. realpath(filename);

用于判断 path 是否真实存在的一个路径

如果不存在，返回的是布尔 false

如果真实存在，那么会将 '/' 转换为 \

如果真实存在，相对路径会转化成绝对路径

```php
$path = 'c:/php9/2020/hello.txt';
echo '<pre>';
print_r(realpath($path)); // true=>c:\php9\2020\hello.txt,'/'转为'\'
print_r(basename($path));//false
```



## 2. 打开文件

### 2.1 fopen(filename, mode);

用于打开一个文件，用于之后文件的操作

​	filename 	是一个表示文件的完整名的一个字符串

​	mode	表示打开的方式

取值：

r	以只读取的方式打开文件，如果文件不存在，则报错

r+	以读写的方式

w	以写的方式打开，如果文件不存在，则创建文件；如果文件存在则清空文件内容

w+ 以读写的方式

a	以追加的方式打开，如果文件不存在，则创建文件；如果文件存在并不会清空文件

a+	追加的方式打开

如果打开成功返回的是一个资源类型

```php
$filename = './test.txt';
$ret = fopen($filename, 'r');
```



## 3. 关闭文件

fclose(handle);

说明：

​	handel 是 fopen()函数函数的资源

```php
$filename = './test.txt';
$ret = fopen($filename, 'r');
fclose($ret);
```



### 4. 写入文件

#### 4.1 fwrite(handle, data);

如果以 r，r+ 打开的文件，那么文件的指针位于文件头部

如果以 a， a+ 打开的文件，那么文件的指针位于文件尾部

```php
$filename = './test.txt';
$handle = fopen($filenmae, 'r+');
fwrite($handle, 'abc');
```



#### 4.2 file_put_contents(filename, data);

用于向文件中写入数据，文件不需要打开，如果文件存在，则清空 //一般用以排错



### 5. 读取文件内容

#### 5.1 fgetc(handle);

​	handle 	是fopen 函数返回的资源类型

​	每次从handle 所代表的文件中 读取一个字符,文件的指针会下移一行

```php
$filename = 'data.txt';
$handle = fopen($filename, 'r');
$chr = fgetc($handle);
while($chr=fgetc($handle)){
    echo $chr;
}
```



#### 5.2 fgets(handle[, len]);

len	表示读取的字节个数，默认是1024，当遇到换行回车时结束读取

```php
$filename = 'data.txt';//abc
$handle = fopen($filename, 'r');
$chr = fgets($handle); //abc
$chr = fgets($handle, 3); //ab,读取len-1个
```



#### 5.3 fread(handle,len);



```php
$filename = 'data.txt';//abc
$handle = fopen($filename, 'r');
$chr = fgets($handle); //abc
$chr = fread($handle, 3); //ab,读取len-1个
```

#### 5.4 file(filename);

filename  	用于表示文件的字符串

将文件中的每一行，读取为数组元素



### 8. 文件的判断

#### is_file(filename); 

主要用于区分文件还是文件夹

### 9. 文件指针

ftell(handle)；	用于获取文件的指针



fseek(handle, n[, whence]); 用于获取文件的指针

​	whence 表示移动的相对位置

​		SEEK_SET	相对于文件头
​		SEEK_END	相对于文件尾
​		SEEK_CUR	相对于当前位置

### 10. 文件锁(了解)

#### flock(handle,type)

​	type 表示锁的类型，取值

​		LOCK_SH	取得共享锁定（读取的程序
​		LOCK_EX 	取得独占锁定（写入的程序
​		LOCK_UN	 释放锁定（无论共享或独占



## 二. 目录操作

### 1. 创建目录

mkdir(path[, mode[, recursive]])

​	path	所要创建的文件夹

​	mode	权限，主要体现在linux

​	recursive	取值为布尔值，表示要创建层级文件夹

```php
mkdir('app/test', 666, true); //resource(3) of type (stream)

```

opendir($handle);



closedir($handle);



### 4. 目录重命名

rename(source, dest);

​	source	原文件夹名

​	dest	新文件夹名

```php
$file = 'data.txt';
rename($file, 'changename.txt');

$dir = 'app';
rename($dir, 'rename');
```



### 5. 删除文件夹名

rmdir(handle)

说明

### 6. readdir($handle);

用于读取当前文件夹内容，不能读取子级文件夹内容，每次读取完，指针下移一行

```php
$dir = 'app';
$handle = opendir($dir);
$item = readdir($handle);
echo $item, '<br/>';	// . 当前文件夹

$item = readdir($handle);
echo $item, '<br/>';	// .. 上级文件夹

$item = readdir($handle);
echo $item, '<br/>';	// 具体文件夹||文件名
```



### 7. 扫描目录

scandir

一次性将文件夹内所有文件读取出来，不包含子文件，返回索引数组



### 8. is_dir();

用于判断给定的是文件还是文件夹