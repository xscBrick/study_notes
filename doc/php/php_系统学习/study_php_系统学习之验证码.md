# study_php_系统学习之验证码

[TOC]

## 什么是验证码

CAPTCHA	全自动区分人与计算机的图灵测试

计算机是可以获取页面上的html 中的信息，但是不能获取谢谢到图片上的文件信息，如果想获取写到图片上的文字信息，必须借助人的眼睛，识别图片上的信息，必须由人为参与

## 作用

用于区分计算机与人，为了降低在很少的时间内对我们站点的一个访问频率

## 制作验证码

将一串随机生成的字符串画到图片上

### 1. 生成随机字符串

```
$charset = 'abcdefghijkmnpqrstuvwxyz'
```



### 2. 绘制验证码



## 验证码应用