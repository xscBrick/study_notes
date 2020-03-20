# study_php_系统学习之绘画技术

[TOC]

## 开启扩展

php 默认是不支持绘画技术，需要我们开启php扩展

```
extension=php_gd2.dll
//extension=gd2
```



## 创建画布

语法： imagecreatetruecolor(w,h);

说明：w 宽， h高

​	返回的是信息资源

示例：

```php
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w,$h);

// var_dump($img); //draw webresource(2) of type (gd)
header('content-type:image/jpeg');
imagejpeg($img);
```



## 分配颜色 imagecolorlocate

imagecolorlocate(img,r,g,b)

说明
	img	画布资源

​	rgb	十进制的画布颜色

```
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w,$h);

//创建一个颜色资源，但是并没有使用
$bg = imagecolorlocate($img, 255, 0, 0);
// var_dump($img); //draw webresource(2) of type (gd)
header('content-type:image/jpeg');
imagejpeg($img);
```

## 填充颜色 imagefill

imagefill(img,x,y,color);

​	img 	画布资源

​	x,y 	画布上某个点

​	color	填充颜色

```php
<?php

// echo 'draw web';
// phpinfo();
$w = 400;
$h = 200;
$img = imagecreatetruecolor($w,$h);

//创建一个颜色资源，但是并没有使用
$bg = imagecolorallocate($img, 255, 0, 0);

//填充颜色
imagefill($img, 0, 0, $bg);

// var_dump($img); //draw webresource(2) of type (gd)
header('content-type:image/jpeg');
imagejpeg($img);
```



## 基本图形的绘制

### 绘制矩形 imagerectangle()

语法：imagerectangle(img,x1,y1,x2,y2,color);

​	rectangle 矩形

​	img	画布资源

​	x1，y1	左上角顶点坐标

​	x2，y2	右下角顶点坐标

​	color	边线颜色

### 绘制直线 imageline

imageline(img,x1,yi,x2,y2,color);



### 绘制字母 imagestring

imagestring(img,size,x,y,string,color);

​	img	画布资源

​	size	文字大小， 0至5个等级

​	x，y	所要绘制位置，坐上角位置

​	string	文字

​	color	颜色



### 绘制汉字 imagettftext

语法： imagettftext(img,size,angle,x,y,color,font,text)

​	size	大小，像素

​	angle	角度

​	x.y	左下角坐标
​	font	所要绘制的内容的字体
​	text	所要绘制的字体





### 输出画布

#### imagejpeg($img[, $filename])

#### imagepng($img[, $filename])

#### imagegif($img[, $filename])

​	$filename	表示所要保存的文件名，可以省略，如果省略则输出到 浏览器

​		在输出到浏览器之前必须设置 `header('content-type:image/jpeg')`
​	在将画布输出到浏览器时们不要有任何多余的输出，如果无法显示图片，需要将 header() 注释掉才可以看到错误信息

### 扩展：

​	windows 操作系统的字体位于 c:/windows/fonts 目录内
​	可以将所需要的字体复制到当前目录来使用



### 从图片创建画布

imagecreatefromjpeg(string($filename))

imagecreatefrompng

imagecreatefromgif

​	以上是所有读取的图片文件

​	以上函数会使用 file 图片的宽高来创建一个画布，并将图片的原内容读取到画布中

注意

​	

getimagesize($file);//返回 imageinfo

