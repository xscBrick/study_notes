# study_html_系统学习之 submit

[TOC]

## 提交按钮 submit

提交按钮的name 属性值，一般情况下不写

因为我们一旦将表单的 控件标签写了name 属性值以后

就表示要将这个表单的控件标签的value 属性值 提交表单的处理程序

什么情况下 需要写name 属性，

凡是需要将这个数据提交给表单的处理程序进行处理的，都需要加name属性

反正不需要交给表单的处理，就可以不写name 属性

## 重置按钮 reset

将表单里面的数据置空

```html
<input type='reset' />
```

## 图片按钮 img

图片按钮是具有表单提交的功能

```
<input type='image' src='./...' />
```

src = 图片地址

## 普通按钮 button

配合javascript 使用，没有表单重置与重置的功能



## 文件上传 file



## 隐藏域 hidden

隐藏域里面的 value 属性值在浏览器上面是看不到的



## `<button>` 标签

建议使用 `<button type="button">提交</button>` input 标签有 浏览器兼容的问题

