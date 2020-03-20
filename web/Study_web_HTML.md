# Study_web_HTML

[TOC]

# HTML 超文本标记语言

**HyperText Transfer Protocal**

网页是基于浏览器的应用程序

浏览器能够识别和解析的语言，通过标签的形式构建页面结构和填充内容

## 标签

标记或元素，标记内容

#### 语法 ：

标签以<>为标志，标签名不区分大小写（建议小写）

#### 标签属性

由属性名和属性值组成，属性值使用 "" , '' 表示，书写在**开始标签**中，使用空格与标签名 隔开，用于设置当前标签的显示内容或者显示效果，同一个标签中可以添加几组标签属性，使用空格间隔

```html
<meta charset="utf-8">
<img src="" width="" height="">
```

##### 注意：注释不能嵌套使用

## 常用标签介绍

### 网页头部设置  head

#### 添加网页标题 title

#### 设置字符集 meta

```
<meta charset="utf-8">
```

#### 设置选项卡小图标 link

```
<link rel="shortcut icon" href="web.ico" type="image/x-icon">
```

#### 外部资源的引入（外部样式表，外部js文件）

#### 网页的说明信息

### 网页的主体部分 body

#### 文本标签

##### 标题标签 h(1~6)

分为六级标题，自带加粗效果，从以及到六级字号逐渐减小

注意：<p>默认页面字体大小为16像素</p>, 一级标题字体大小为32像素

##### 段落标签 p

##### 普通文本标签

###### span:  行分区标签，用于为特殊文本添加样式

###### label： 结合表单控件实现文本与按钮的绑定

###### b 或者 strong：

b :  无语义标签

strong : 有语义标签

###### i : 斜体展示

###### s : 删除线

###### u: 下划线

###### sup: 上标

###### sub ： 下标

##### 格式标签

###### hr 或 hr/   :水平线标签

###### br 或 br/ :  换行标签

注意： 浏览器会忽略代码中多余的换行和空格，解释为一个空格

##### 字符实体

带有特殊意义的符号

```
1. < : &lt;
2. > : &gt;
3. © ：&copy;
4. ¥ ：&yen;
5. 空格 ：&nbsp;
```

### 容器标签 div

用于页面结构的划分

### 列表标签

#### 有序列表

```html
<ol>
    <li>list item 列表项</li>
    <li>list item 列表项</li>
    <li>list item 列表项</li>
</ol>
```



#### 无序列表

```html
<ul>
    <li>list item 列表项</li>
    <li>list item 列表项</li>
    <li>list item 列表项</li>
</ul>
```

#### 列表的标签属性

##### 有序列表 ol

###### type 属性

设置项目符号类型

###### 取值：

```
1 2 3 4 
a b c d
A B C D
i ii iii iv
I II
```

###### start 属性

设置从第几个符号开始

##### 无序列表 ul

###### type 属性 设置项目符号类型

###### 取值

```
disc 默认值， 实心圆点
square 实心方块
circle 空心圆
none 取消项目符号
```



#### 列表的嵌套



### title 属性 传入变量

```javascript
cidr_info =  '<td>' + data[item]['subnet']+ "/" + data[item]['intMask']+ '(主)' + '<a href="#" class="more_info_link cidr_info" title = "'+ title_info +'" >'+ data[item]['assistCidrs'].length + '</a></td>';
```

### 图片与超链接

#### 路径 URL

url 统一资源定位符 资源文件的所在位置

组成： 
协议， 域名， 目录， 文件名

https：//baike.baidu.com/item/.../..?..

### 图片标签 img

属性：

#### src ： 必填属性，设置图片 URL

#### width/height：取像素值，设置图片尺寸

选填，默认图片按照原始尺寸显示到页面中，可以通过width/height 手动设置图片宽高，取像素值，如果只设置宽或高，另外一个方向的尺寸会等比缩放

#### title 设置图片标题

#### alt : 设置图片加载失败时 的提示文本

### 超链接标签 a

作用：连接到指定文件（指定位置）

#### 语法： 

```html
<a href="">超连接文本</a>
```

#### 属性：

##### href : 

必填，省略的话与普通文本没有区别，用来设置超链接的链接地址

href 的取值：

href = "" 表示链接到本页，相当于刷新

href = "javascript:void(0)" 表示链接到本页，不刷新

href = "#" 表示链接至本页，会在当前的url 后面添加# ，改变了url， 不刷新

href = "路径"  网络路径必须写协议

#####  target

设置目标文件的打开方式，默认在当前窗口打开

取值：

_self : 默认值，在当前窗口打开
_blank : 新建窗口打开

#### 样式：

超链接文本都自带下划线，分为不同状态

访问前 默认为蓝色文本，

访问后： 默认为紫色文本

#### 锚点链接：

作用：链接至指定文件的指定位置，#是锚点的标志

语法：
1.页面中添加锚点：

借助于空的 a 标签，通过name 属性定义锚点名称

```html
<a name="7"></a>
```

2.设置锚点链接地址

```html
<a name="7"></a>
<a href="#7">7.人物评价</a>
```

### 表格标签 table

#### 作用：

通过结构话的行和列 （单元格）实现辅助排版或数据展示

#### 语法：

```html
<table><--!表示表格-->
    <tr>表示一行（table row）</tr>
    <td>表示一列，单元格，展示数据（table data）</td></td>
</table>
```

#### 属性：

##### table 标签属性

```
border : 取像素值，为表格添加边框（单元格也会被加上边框）
bgcolor : 取颜色值，可使用英文单词,设置表格背景颜色
cellspacing : 取像素值,设置边框与边框之间的距离
cellpadding : 取像素值,设置内容框与边框之间的距离
width/height : 取像素值,设置表格尺寸,默认表格大小由内容的多少决定
align : 取值 left(默认)/center/right,设置表格在其父元素中的水平对齐方式
```

##### tr 的标签属性

```
bgcolor : 设置当前行的背景颜色
align : 设置当前行中内容的水平对齐方式,取值left(默认值)/center/right
valign : 设置当前行中内容的垂直对齐方式,取值top/middle(默认值)/bottom
```

##### td 的标签属性

```
bgcolor : 设置单元格背景颜色
align : 内容的水平对齐方式
valign : 内容的垂直对齐方式
width/height : 设置单元格尺寸
```

#### 单元格合并 表格结构调整

##### 跨列合并 colspan 

为单元格添加 colspan 属性， 取无单位的数值，表示包含自身在内合并几个单元格

##### 跨行合并 rowspan 

为单元格添加 rowspan 属性，取无单位的数值， 表示包含自身在内向下合并几个单元格

注意：
不管是跨行还是跨列，都涉及代码中单元格数量的调整
跨列合并，影响当前行中的单元格，需要删除当前行中多余的单元格

跨行合并，影响其后行中的单元格，需要依次到行中删除被合并的单元格

#### 表格行分组

##### thread 表头分组

可以嵌套若干行，表示表头

##### tfoot 表尾分组

可以嵌套若干行，表示表尾

##### tbody 表格主体行分组

默认书写的所有tr，td 都会自动加入 tbody 中，作为表格主体内容

### th 标签

用法与td 一致，表示单元个，常用于表头单元格，自带加粗和文本水平居中效果

### 表单标签 form

#### 作用：

表单用于收集用户信息i叫给服务器

#### 组成：表单元素和表单控件

##### 表单元素 <form></form> 负责提交数据

##### 表单控件用于收集数据（输入框，单选钮，复选框等）

语法实例： 

```html
<form>
    表单控件
</form>

```

#### form 标签属性

##### action ： 设置数据的提交地址

##### method ： 设置数据的提交方式，默认为get

###### method = "get"

数据将以铭文的方式，拼接在url 后面进行提交；
安全行较低；
数据大小有一定限制，不超过2kb

###### method = "post" 

数据会被打包发送，跟随请求头，请求体一并传输；
安全性较高；
数据传输大小没有限制，可以传输二进制数据（图片，文件，音视频）

##### enctype ： 指定数据法网服务器时的编码类型

取值：

###### application/x-www-form-urlencoded

默认值，对应get请求，将表单中的数据转换成字符串，以参数的形式拼接在url后面

###### multipart/form-data

用于特殊数据类型的传输，对应post 请求，用于传输图文，文件，音视频等二级制数据

#### 表单控件 （重点）

提供一系列可视化的组件，用于数据数据

分类

##### 文本框与密码框 input type=text / password

```html
<input type="text">文本框
<input type="password">密码框

```

标签属性：
type ： 必填， 设置控件类型
name ： 设置控件名称（不能使用name）

value ： 控件的值
placeholder ： 用户输入之前的提示文本

maxlength :  设置最大输入长度

##### 单选钮和复选框 input type=radio / checkbox

语法：

```html
<input type="raido" > 单选钮
<input type="checkbox"> 复选框

```

属性：
type ： 必填项，指定控件类型

name :  必填项，指定控件名称，同一组按钮的控件名称必须保持一致

value ： 必填项，表示控件的值

checked  : 设置按钮的默认选中状态
	checked="checked" 简写为checked

##### 文本与控件的绑定

label for id 用法

将文本使用label 标签表示

为相应的控件添加id 属性， 属性值自定义，id属性具有唯一性

为label 添加 for 属性，属性值为对应控件的 id值

#### 隐藏域和文件选择框

##### 文件选择框 input type="file"

```html
<input type="file" name="">

```

文件包含图片，文本文件，音视频文件

需要注意：

数据提交方式必须为post 

编码类型必须设置： enctype="multipart/form-data"

##### 隐藏域 input type="hidden"

用户不可见， 用于设置用户不关心， 服务器需要的数据

```html
<input type="hidden" name="uid" value="001">

```

#### 下拉菜单 select

```html
<select name="address">
    <option value="beijing">北京</option>
    <option value="shanghai">上海</option>
</select>


```

默认选中第一个ption, 可以通过属性 selected设置某个选项默认选中

#### 多行文本域 textarea

```html
<textarea name="uinfo"></textarea>

```

支持多行输入，可以由用户调整尺寸

#### 功能按钮 submit / reset / button 

##### 提交按钮 submit

当用户点击提交时，会将数据按照指定的方式和指定的地址发送给服务器

```html
<input type="submit" value="">

```

value 属性用来设置按钮的显示文本

##### 重置按钮 reset

将表单中的数据还原到初始化状态

```html
<input type="reset" value="">

```

##### 普通按钮 type=button

需要通过js 绑定自定义事件

事件： 用户行为（鼠标操作，键盘操作）

```html
<input type="button" value="">

```

注意：普通按钮没有默认显示文本，必须通过value设置

##### 按钮标签 button

```html
<button>
    点击
</button>

```

标签内容就是按钮的显示文本
书写在表单外，相当于普通按钮，需要自定义事件，书写在表单内，相当于提交按钮

### html title换行

```html
<!--直接换行-->
<a href="#" title="1
2
3
4">html title换行(直接换行)</a>

<!--换行符换行-->
<a  href="#" title="1&#13;2&#13;3&#13" >html title换行(换行符)</a>

```

