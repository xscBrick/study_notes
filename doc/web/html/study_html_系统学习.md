# study_html_系统学习

[TOC]

## HTML 简介

超文本标记语言 

标记：当浏览器遇到相应标签时实现相应的功能



## 标签

### 双边标签



### 单边标签

只有开始没有结束

其内容再标签属性中赋值，某一些单边标签如果要显示内容，需要将内容放置再单边标签里面的 value 属性中

```html
<input type="text" value="按钮" />
<br />
```

### 属性

属性一般是用于来描述这个标签有什么



## 文本修饰标签

b & strong  加粗， strong强调的程度更强一些



我们可以将html 网页理解为一个已经装修好的房子



## 排版标签

###  排版标签之 h 标签

![image-20200318095359689](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200318095359689.png)

由于h 元素标签 有明确的语义，因此请您慎重的选择恰当的层级来构建文档的解结构，请不要利用标题标签来改变同一行中的字体大小，相反，我们应该使用层叠样式来定义来达到漂亮的显示效果

align 排列

设置标题标签里面的文本的水平方向的对齐方式

h1 标签非常重要，在一个html 文件中 h1 标签必须要是唯一



### 排版标签之 p 标签 段落

段落标签

### 排版标签之 hr 横线

```
hr color="yellow" width="800" size="40"
```

color	颜色

width	宽度 像素或者百分比(父元素百分比)

size 粗细

align	设置水平方向的对齐方式，

noshade	去掉水平线的阴影的效果，这个属性本身没有属性值，如果属性没有值，那么属性的值等于其本身



### 排版标签之 pre 定义预格式化的文本

# cookies

快捷键

```
h${标题$}*6 + tab    //$顺序

```



### 字符实体

在html 中 某些字符是预留的

![image-20200318232727460](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200318232727460.png)



### DTD document type defincation

html5	--> <!DOCTYPE html>

## 列表标签 

### 列表标签 之 无序列表 ul li

ul : 无序列表 unordered  list 

li: 列表项list item

ul属性

![image-20200319000836028](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200319000836028.png)

#### 列表嵌套



### 列表标签 之 有序列表 ol li

type 属性 A a i I 1

start 属性



###  列表标签 之 定义列表 dl dt dd

definition list

dt: title 定义标题

dd: description 对定义标签进行描述，解释说明



## 图片标签 img

能够使用的图片类型

src属性 资源 source

alt属性 alternate 替换，表示当图片资源加载不成功的时候显示的文字信息

title属性，放在图片上显示的文字信息



## 表格标签 table

>```
>color
>border
>bordercolor
>width
>height
>background	设置背景图片
>cellspacing	设置单元格与单元格之间的距离
>cellpadding 单元格里面的内容到边框线之间的距离
>rules 取值：all 就表示将表格的边框线合并
>align 	设置表格的水平位置
>```
>
>



### 表格标签 之 行标签 tr

```
高度	height 给行设置宽度
背景颜色	bgcolor	给行设置背景颜色
背景图片	background	给行设置背景图片
水平对齐方式	align 	设置行里面内容的水平对齐方式
垂直对齐方式	calign	设置行里面内容的崔志对齐方式	top middle bottom
```



###  表格标签 之 列标签 td th

# cookies

## 标准属性



## 事件属性



![image-20200319003240635](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20200319003240635.png)