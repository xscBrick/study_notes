# php 字符串长度截取

[TOC]

substr, mb_substr,mb_struct



## substr(字符串， 开始位置从0开始，截取长度);

如果字符串是 多个字节 比如中文，会出现乱码 适用于字母和数字

```php
$str = 'abctestdef';
echo substr($str, 3, 4); //test
```



### mb_substr(字符串,开始位置,截取长度,字符编码)

适用于截取中文，按字来切分

```php
echo mb_substr('很好用nice',0,3,'utf-8'); //很好用
```



### mb_strcut(字符串,开始位置,截取长度,字符编码)

按照字节来切分

```php
echo mb_strcut('很好用nice',0,3,'utf-8'); //很
```