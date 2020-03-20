# Study_web

[TOC]

web:  HTML,  CSS,  JS,  Jquery,  flask, Django
网页是基于浏览器的应用程序

> B-S :  Browser/ server  浏览器与服务器交互模式
>
> C-S : Client / Server  客户端与服务器交互

#### 组成：

##### 浏览器：

1.代替用户发请求（用户代理）
2.解析数据并呈现给用户

##### 服务器：

1.存储数据

2.处理并响应请求

##### 协议

通信协议, 规范数据在传输过程中以何种形式传递（HTML）

#### 产品

#### 1.浏览器

Chrome  - Google
IE / Edge - Microsoft
Safari - Apple
FireFox - Mozilla
Opera - Opera
引擎 ：
渲染引擎：关系整个页面的渲染
JS引擎：对JS代码的处理

#### 2.服务器

Apache
Tomcat
IIS - Internet Information Service
Nginx

# HTML

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



#  CSS

# Study_web_CSS

[TOC]

层叠样式表 cascading style sheets

HTML 负责书写页面结构和内容，CSS负责排版布局和样式美化

使用方式

### 行内样式/内联样式

#### 语法：借助于style 标签属性，为标签添加样式

<标签名 style="样式声明">

CSS 样式声明 ： 由 CSS 属性和值组成

​	style="属性:值; 属性:值;"

##### 常用CSS 属性：

设置文本颜色： color:red;

设置背景颜色： background-color:green;

设置字体大小 : font-size:32px;

### 内嵌样式

借助于 <style type="text/css"></style >标签，在文档中嵌入 CSS 样式

```html
<head>
    <style type="text/css">
        h1{
            color:green;
            background-color:orange;
        }
        div{
            color:red;
            font-size:40px;
        }
        p{
            color:black;
            fon-size:16px;
        }
    </style>
</head>
<body>
   	<h1>
        一级标题
    </h1>
    <p style="color:red; font-size:32px;">
        行内样式
    </p>
    <p>
        参考
    </p>
    <div>
        <span>span</span>
    </div>
</body>
```

### 外链样式表  .css

创建外部样式表文件， 后缀使用 .css

在HTML 文件中引入外部样式表

<link rel="stylesheet" href="URL" type="text/css">

样式表文件中借助选择器匹配元素应用样式

### 样式表特征 

#### 层叠性

多组CSS 样式共同作用于一个元素

#### 继承性

后代元素可以继承祖先元素中的某些样式

#### 样式表的优先级

优先级用来解决样式冲突问题

同一个元素的同一个样式（例如文本色），在不同地方进行设置，最终选用哪一种样式？

> 行内样式的优先级最高
>
> 文档内嵌与外链样式表，优先级一致，看代码的书写顺序，后来者居上
>
> 浏览器默认样式和继承样式优先级较低



### 选择器

作用：
匹配文档中的某些元素为其应用样式

分类：

#### 标签选择器

根据标签名匹配文档中所有该元素
语法：

```html
标签名{
	属性：值;
}
h1{
	color:red;
}
```



#### id选择器 #

根据元素的id属性值匹配文档中唯一元素，id具有唯一性

语法：

```html
<head>
    <style>
        #id属性{	
            属性:属性值;
        }
        #d1{
            color:red;
        }
    </style>
</head>

<body>
    <div id="box">
        <p class="c1" id="d1">
            段落
            <span>span</span>
        </p>
    </div>
</body>
```

注意：

id属性值自定义，可以由数字，字母，下划线，-组成，不能以数字开头，
尽量见明知意，多个单词组成时，可以使用连接符，下划线，小驼峰表示

#### class选择器/类选择器 .class

根据元素的class 属性值匹配相应的元素，class 属性可以重复使用，实现样式的复用

语法：

```html
.class属性值{
	
}
```

特殊用法：
1.类选择器与其他选择器结合使用

注意标签与类选择器结合时，标签在前，类选择器在后

a.c1{}

class属性值可以写多个，共同应用类选择器的样式

.c1{}

.c2{}

<p class="c1 c2"></p>

#### 群组选择器 selector

为一组元素统一设置样式

语法: 

```html
selector1,selector2,selector3{

}
div p span{
color:red;
}
```



#### 后代选择器

匹配满足选择器的所有后代元素（包含直接子元素和简介子元素）
语法：selector1 selector2{}

匹配selector1 中所有满足 selector2的后代元素

#### 子代选择器

匹配满足选择器的所有直接子元素

语法：
selector1>selector2{ }

#### 伪类选择器

为元素的不同状态分别设置样式，必须与基础选择器结合使用

分类：

##### :link	超链接访问前的状态

##### :visited	超链接访问后的状态

##### :hover	鼠标滑过时的状态

##### :action	鼠标点按不抬起时的状态（激活）

##### :focus	焦点状态(文本框被编辑时就称为获取焦点)

```html
a:link{

}
a:visited{

}
.c1:hover{}
```

注意：
超链接如果需要为四种状态分别设置样式，必须按照以下顺序书写：
:link
:visited
:hover
:action
爱恨原则：LoVeHAte

超链接常用设置：
a{

统一设置超链接默认样式(部分状态)

}

a:hover{

鼠标滑过时改样式

}

### 选择器优先级

使用选择器为元素设置样式，发生冲突时，主要看选择器的权重，权重越大，优先级越高

| 选择器       | 权重 |
| ------------ | ---- |
| 标签选择器   | 1    |
| (伪)类选择器 | 10   |
| id选择器     | 100  |
| 行内样式     | 1000 |

复杂选择器(后代，子代，伪类) 最终的权重为各个选择器权重值之和群组选择器以每个选择器的单独的权重为准，不进行相加计算

## 标签分类及嵌套

### 块元素

独占一行，不与元素共行，可以手动设置宽高，默认宽度与父元素保持一致

body div h1~h6 p ul ol li form table(默认尺寸由内容决定)

### 行内元素

可以与其他元素共行显示，不能手动设置宽高，尺寸由内容决定

span label   strong i s u sub sup a

### 行内块元素

可以与其他元素共行显示，又能手动调整宽高，

img 	input button （表单控件）

### 嵌套原则

块元素可以嵌套任意类型的元素

​	p元素除外，段落标签只能嵌套行内元素，不能嵌套快

行内元素中只能嵌套行内或行内块元素

## 尺寸与颜色值

### 尺寸单位

>1. px : 像素,默认单位
>2. %  : 百分比,参照父元素对应的尺寸计算
>3. em : 相对父元素的字体大小进行计算,默认字体大小为					16px, 1em=16px
>4. rem : 相对页面的根元素的字体大小进行计算,默认16px

### 颜色表示

#### 颜色英文单词表示

#### rgb(r,g,b)方法	:

使用三原色表示,每种颜色取值范围为	0~255,值越大,越饱和

```
white rgb(255,255,255)
black rgb(0,0,0)
red   rgb(255,0,0) 红
green rgb(0,255,0) 绿
blue  rgb(0,0,255) 蓝
```

####  rgba(r,g,b,alpha)方法:

```
r,g,b表示三原色取值范围0~255
alpha表示透明度,取值范围 0(透明)~1(不透明)
例 :
rgba(255,0,0,0.5)
rgba(255,0,0,.5)
注意 :
所有元素默认背景色都为透明
窗口的白色是浏览器渲染的结果
```

#### 十六进制

```
以#为前缀,分为六位的十六进制和三位的十六进制
六位十六进制 :
每两位为一组代表一种三元色
每位的取值范围 : 0~9 a~f
例 :
    #ff0000  rgb(255,0,0)
    #ffffff  白
    #000000  黑
三位十六进制 :
简化书写,每一位就代表一种三元色
浏览器会自动对每一位进行重复,补全成6位的十六进制
例 :
    #f00
    #0f0
    #000
    #fff
```

### 内容与边框

#### 内容尺寸及溢出处理

```
尺寸 :
	width/height : 设置元素宽高
内容溢出 :
内容超出元素尺寸范围称为溢出,默认情况下,溢出部分仍然可见,影响其他元素正常显示,可以借助overflow调整溢出内容的展示
属性 : overflow
取值 :
    visible (默认可见)
    hidden  (隐藏溢出部分)
    scroll  (强制添加水平和垂直方向的滚动条)
    auto		 (自动在溢出方向添加可用的滚动条)
```

#### 边框设置

##### 边框实现

```
属性 : border
取值 : width style color;(属性值之间用空格隔开)
border-width : 取像素值,设置边框宽度
border-style : 设置边框样式,可取
    solid  实线
    dashed 虚线
    dotted 点线
    double 双线
border-color : 设置边框颜色,取颜色值
注意 :
边框宽度默认为3px,边框颜色默认为黑色
边框的样式没有默认值,必须指定
```

##### 单边框设置

```
border属性用于统一设置上右下左四个方向的边框样式
单边框设置
    border-top    上边框
    border-right  右边框
    border-bottom 底部边框
    border-left		左边框
属性取值与border一致 : width style color;
```

#####  网页三角标设置

```
步骤 :
1. 块元素设置宽高为0
2. 统一设置四个方向边框宽度,样式和透明色
(三角标依据边框拼接得到,不能随意省略边框)
3. 调整某方向边框为可见色
```

#####  轮廓线

```
轮廓线与边框类似,但是轮廓线在页面中不占据实际尺寸,边框会实际占位
属性 : outline
取值 : color style width;
注意 :
	取值为none可以取消默认的轮廓线(文本框)
```

##### 圆角边框

```
属性 : border-radius
取值 :
取像素值,表示固定以给出的半径在四个角做圆角
取百分比,参照元素本身的尺寸计算半径(计算长短轴)
取值情况 :
1. 像素值
    border-radius : 20px; 
    统一设置上右下左四个角的圆角程度
    border-radius : 10px 20px 30px 40px;
    分别设置上右下左四个角的圆角程度
    border-radius : 10px 20px;
    设置上下角为10px,左右角为20px
    border-radius : 10px 20px 30px;
    分别设置上下两个角,左右一致
    等价于 10px 20px 30px 20px;
2. 百分比
    属性值可取1/2/3/4个值,与像素值使用一致
    注意 :
    1. 统一设置四个角的圆角效果时,最大取50%
    50% 会改变元素形状(圆/椭圆)
    >50% 仍然表现为50%的效果
    2. 单独设置每个角的圆角效果,取值0%~100%
```

##### 盒阴影

```
属性 : box-shadow
取值 : offsetX offsetY blur (spread) color;
offsetX : 取像素值,表示阴影的水平偏移距离
正值表示向右偏移,负值表示向左偏移
offsetY : 取像素值,表示阴影的垂直偏移距离
正值表示向下偏移,负值表示向上偏移
blur		: 取像素值,表示阴影的模糊程度,值越大,						越模糊
spread	: 取像素值,表示阴影的延伸距离(选填)
color		: 设置阴影颜色,默认为黑色
注意 :
不管是浏览器窗口还是页面元素都带有坐标系,一律以左上角为(0,0)点,向右向下分别为X轴和Y轴的正方向.默认元素都从左上角开始显示
```

###  盒模型	

1. 理解盒模型的组成及相关属性,可以更好的实现元素排版布局.盒模型相关的属性会影响元素在文档中的最终占据尺寸.
2. 组成及计算

##### 组成 :

内容框   width / height
内边距	 padding(内容与边框之间的距离)
边框		 border
外边距	 margin(元素边框与边框之间的距离)

##### 计算元素最终尺寸

标准盒模型下,元素最终占据的宽高由盒模型各属性值相加得到
特殊元素的计算方式除外

3. 外边距(margin)

用来设置元素与元素之间的距离
取值 : 像素值
    margin : 10px; 统一设置上右下左为10px的外边距
    margin : 10px 20px; 上下为10px,左右为20px
    margin : 10px 20px 30px; 上下分别为10,30,左右一致					 为20
    margin : 10px 20px 30px 40px;分别设置上右下左四个					 方向的外边距
特殊值 :
    1. margin : 0; 取消默认外边距
        2. margin : 10px auto; 表示左右自动外边距,实现元素的水平居中
        3. 取负值,表示元素位置的微调
单方向外面距的设置
	属性 : 
        margin-top
        margin-right
        margin-bottom
        margin-left
	取值 : 一个像素值
外边距合并
	1. 垂直方向
		1. 子元素设置的margin-top作用于父元素上
		解决 :
            1. 为父元素添加顶部边框
            2. 为父元素添加0.1px的padding-top
		2. 垂直方向上,两个元素同时添加上下外边距,发生合并,取较大的值
	2. 水平方向
        水平方向上的外边距会叠加显示
        行内元素对盒模型属性不完全支持,不支持width/height,不支持上下的边距设置
默认带有外边距的元素:
body,h1,h2,h3,h4,h5,h6,p,ul,ol{
margin:0;
}

4. 内边距(padding)
   设置元素内容框与边框之间的距离
   取值 :
   padding : 10px;
   padding : 10px 20px;
   padding : 10px 20px 30px;
   padding : 10px 20px 30px 40px;
   padding : 0; 清除默认内边距
   单方向内边距的设置
   属性 :
   padding-top
   padding-right
   papdding-bottom
   padding-left
   取值 : 一个值
   具有内边距的元素 :
   ol,ul,input,button
   一般将列表的内外边距都设置为0
5. 盒模型计算
   属性 : box-sizing
   作用 : 设置盒模型的计算方式
   取值 :
6. content-box
   默认值,除表单元素外,大多采用默认的计算方式
   元素最终在文档中的尺寸由盒模型属性值依次相加得到
   width/height设置的尺寸对应为元素内容框的大小
7. border-box
   width/height设置的尺寸对应为边框区域的大小
   width/height实际包含边框+内边距+内容
   元素最终在文档中的占位 :
   margin + width/height
   练习 :
   创建div(普通元素) 文本框 按钮
   添加尺寸,内边距,边框,外边距
   对照盒模型,观察元素在文档中的最终尺寸
   借助box-sizing,修改盒模型计算方式
   观察元素最终尺寸变化

```
day05

```

### 背景属性

#### 背景颜色

background-color

#### 背景图片相关

##### background-image:url("路径")  设置背景图片

设置背景图片，指定图片路径，如果路径中出现中文或空格，加引号

如果元素尺寸大于图片尺寸，会自动重复平铺，直至铺满整个元素

如果元素尺寸小于图片尺寸，图片默认从元素左上角开始显示，超出部分不可见

##### background-repeat 设置背景图片的重复方式

取值：

repeat  默认值，沿水平和垂直方向重复平铺
repeat-x 沿X轴重复平铺
repeat-y 沿Y轴重复平铺
no-repeat 不重复平铺

##### background-size 	设置背景图片尺寸

取值：width height

表示方法：
	像素值：

​		1.500px 500px;同时指定宽高

​		2.500px；指定宽度，高度自适应

​	百分比：50% 50%;  50%

​		百分比参照元素的尺寸进行计算



##### background-position  设置图片的显示位置，默认显示在元素左上角

取值： x y;

表示方位：

像素值：
方位值：

​	水平：left/center/right
​	垂直：top / center / bottom

百分比：
0% 0%;左上角

100% 100%；右下角

### 精灵图技术：

为了减少网络请求，可以将所有的小图标拼接在一张图片上，一次网络请求得到全部；借助于 background-postion 进行背景图片位置的调整，实现实现不同的图标

#### 简写属性

##### background:color url() repeat position;

```
注意 ：
1. 如果需要同时设置以上属性值，遵照相应顺序书写
2. background-size 单独设置

```

### 文本属性

#### 1. 字体相关

```
1. font-size 设置字体大小
2. font-weight 设置字体粗细程度
取值 ：
1. normal（默认值）等价于400
2. bold   (加粗)	 等价于700
3. font-style	设置倾斜、斜体
取值 ：
1. normal （默认值）
2. italic	 (斜体)
3. oblique (倾斜)
4. font-family 设置字体名称
取值 :
1. 多种字体名称之间使用逗号隔开
2. 如果字体名称为中文,或者名称中出现了空格,必须使用引号
例 :
font-family:Arial;
font-family:"黑体","Microsoft YaHei",Arial;
可以指定多个字体名称作为备选字体
5. 字体简写
font : style weight size family;
注意 :
1. 如果四个属性值都必须设置,严格按照顺序书写
2. size family 是必填项

```

#### 2. 文本样式

```
1. 文本颜色
color 属性取颜色值
文本属性大多都可以被继承(font color等)
超链接的文本色不能由继承得到,只能单独设置
2. 文本装饰线
属性 : text-decoration
取值 :
1. underline		下划线
2. overline			上划线
3. line-through 删除线
4. none					取消装饰线
3. 文本内容的水平对齐方式
属性 : text-align
取值 : left(默认值)/center/right
4. 行高
属性 : line-height
作用 : 指定一行文本的高度
取值 : 像素值
使用 :
文本在当前行中永远垂直居中,可以借助行高调整文本在元素中的垂直显示位置
line-height = height 设置一行文本在元素中垂直居中
line-height > height 文本下移显示
line-height < height 文本靠上显示
特殊 :
line-height可以采用无单位的数值,代表当前字体大小的倍数,以此计算行高
font属性简写
font : size/line-height family;

```

### 3. 表格属性

```
1. table标签是块元素,支持宽高设置,边框设置,边距设置
2. table独有CSS属性
1. 边框合并
属性 : border-collapse
取值 : 
separate 默认分离边框
collapse 设置合并边框
2. 设置边框之间的距离
属性 : border-spacing
取值 : h v;
分别设置水平和垂直方向上边框之间的距离,取像素值;只取一个值表示统一设置水平和垂直两个方向的边距
注意 : 只能在边框分离状态下使用
3. 表格尺寸	
1. 表格采用border-box计算尺寸,默认情况会自动分配单元格的大小
2. 如果单元格和表格同时设置尺寸,表格宽度不受影响,高度会被跟随单元格改变
3. 单独为某个单元格设置尺寸,会影响其所在的行和列;
其他单元格的尺寸仍由表格自动分配

```

### 4. 过渡属性

```
1. 不同状态之间切换样式时增加平滑过渡效果
2. 属性 
1. 指定过渡时长
transition-duration
取值 : 以s(秒)或ms(毫秒)为单位的数值
1s = 1000ms
注意 : 过渡属性一般书写在元素的默认样式中,状态切换的反复过程中,都会添加过渡效果;如果过渡属性书写在hover状态中,只会在默认到hover之间添加过渡效果
2. 指定添加过渡效果的CSS属性
transition-property
取值 : CSS属性名,属性名,属性名;
作用 : 设置哪些CSS属性添加过渡效果;该属性可以省略,表示所有发生属性值改变的样式,都将添加过渡效果
特殊值 :
all 代表所有CSS属性
3. 指定过渡效果的速度变化
transition-timing-function
取值 :
1. ease 默认值 ,慢速开始,中间加速,慢速结束
2. linear 匀速变化
3. ease-in 慢速开始,加速结束
4. ease-out 快速开始,慢速结束
5. ease-in-out 慢速开始和结束,中间过程先加速再减速
4. 设置延迟
transition-delay
取值 : 以s或ms为单位的数值
表示延迟多久发生
3. 简写属性
transition : property duration timing-function delay;
注意 : 过渡时长为必填项
例 :
transition : 5s;
transition : width 5s;
transition : width 5s linear 1s;

```

### 5. 布局方式

```
1. 调整元素的显示位置
2. 布局方式分类 :
1. 文档流/标准流/静态流
默认的布局方式,按照代码的书写顺序和标签类型,从上到下,从左到右依次显示
2. 浮动布局
属性 : float
取值 : none(默认值)/left/right
特点 : 
1. 元素设置浮动,会脱离文档流,表现为悬浮在其父元素的上方;
2*. 浮动元素脱离文档流,在文档中不再占位
3. 浮动元素会按照浮动方向停靠在其他元素的边缘,多个元素设置浮动时,会依次停靠在前一个元素的边缘,一行放不下会自动换行
4. 浮动元素会从它在文档中的起始位置脱流,向左或向右浮动
5*. 元素一旦浮动,就具有块元素的特征,可以手动设置宽高
6*. 文字环绕效果: 浮动元素会遮挡正常元素的位置,不影响正常元素内容的显示,内容会围绕在浮动元素周围

```

#### 1. 标准流/静态流

#### 2. 浮动布局 float

```
属性 : float
取值 : left/right
特点 :
1. 元素设置浮动会从原始位置脱流,向左或向右依次停靠在其他元素边缘,在文档中不再占位
2. 元素设置浮动,就具有块元素的特征,可以手动调整宽高
3. "文字环绕":浮动元素遮挡正常元素的位置,无法遮挡正常内容的显示,内容围绕在浮动元素周围显示
问题 :
子元素全部设置浮动,导致父元素高度为0,影响父元素背景色和背景图片展示,影响页面布局
解决 :
1. 对于内容固定的元素,如果子元素都浮动,可以给父元素固定高度(例:导航栏)
2. 清除浮动
属性 : clear
取值 : left/right/both;
使用 : 正常元素添加clear属性设置,不受前面左浮元素的影响或右浮元素的影响
解决父元素高度为0 :
1. 在父元素的末尾添加空的块元素
2. 设置空的块元素clear:both;
3. 借助overflow:hidden;
为父元素设置overflow:hidden;解决高度为0


```



#### 3. 定位布局 position

```
属性 : position
取值 : static(默认值)/relative/absolute/fixed
只有元素设置relative/absolute/fixed,才能称为已定位元素
分类 :
1. relative 相对定位
特点 : 元素设置相对定位,可参照元素在文档中的原始位置进行偏移,不会脱离文档流
偏移属性 :
top :   距上
right : 距右
bottom :距底部
left :	距左
注意 : 偏移属性可以实现元素位置的调整,只有已定位的元素可以使用偏移属性
2. absolute 绝对定位
特点 : 
1. 绝对定位的元素参照离他最近的已经定位的祖先元素进行偏移,如果没有,则参照窗口进行偏移
2. 绝对定位的元素会脱流,在文档中不占位,可以手动设置宽高
使用 :
1. "父相子绝" : 父元素设置相对定位,子元素参照已定位的父元素偏移.
2. 脱流元素中设置margin,不能使用auto
3. fixed		固定定位
特点 :
1. 参照窗口进行定位,不跟随网页滚动而滚动
2. 脱离文档流
使用 :
1. 聊天窗
2. 广告位
3. 目录位
堆叠次序 :
属性 : z-index
取值 : 无单位的数值,数值越大,越靠上
注意 :
1. 只有定位元素可以使用z-index
2. 父子关系不能使用z-index调整堆叠次序,永远是子元素在上

```

### 转换属性

1. 设置元素的平移,旋转,缩放效果
2. 属性 : transform
3. 取值 : 转换函数
4. 转换基准点

```
默认以元素中心点作为转换基准点
属性 : transform-origin
取值 : X Y;
1. 像素值
在元素自身坐标系中选取基准点
2. 百分比
参照元素尺寸计算坐标点
3. 方位值
水平 : left/center/right
垂直 : top/center/bottom

```



5.转换函数

```
1. 平移
函数 : translate(h,v)
取值 :
函数中传递两个值,分别代表水平和垂直的偏移距离;正值表示沿坐标轴的正方向偏移,负值表示负方向偏移
相关函数 :
translateX(value) 沿X轴平移
translateY(value) 沿Y轴平移
translate(value)  表示沿X轴平移
2. 缩放
转换函数 : scale(value)
取值 :
1. value为无单位的数值,表示缩放比例
2. value > 1 放大
3. 0 < value < 1 缩小
4. value < 0 取负值,数值仍然表示缩放比;负号表示反转元素 
例 : 1 -> 0 -> -1
相关函数 :
scaleX(value) 沿X轴缩放
scaleY(value) 沿Y轴缩放
scale(value)  同时沿X轴和Y轴缩放
3. 旋转
转换函数 : rotate(value)
取值 :
1. 以deg为单位的数值,表示角度
2. 正值表示顺时针,负值表示逆时针;不同的转换基准点,最终效果不同]
相关函数 :
3D转换
rotateX(value) 沿X轴旋转
rotateY(value) 沿Y轴旋转
4. 组合使用
transform : 函数1 函数2;
注意 : 
旋转变换会连带元素的坐标轴一起旋转,影响平移的结果
代码书写顺序不同,最终转换结果不同
例 : 
transform : rotate(45deg) translate(100px);
transform : translate(100px) rotate(45deg);

```

### 元素显示效果

```
1. display
取值 : block/inline/inline-block/none;
作用 : 改变元素类型
block  块元素
inline 行内元素
inline-block 行内块元素
none   隐藏元素
2. visibility
取值 : visible(可见) / hidden(隐藏)
与display:none;设置元素隐藏的区别 :
1. display:none;元素隐藏不占位
2. visibility:hidden;元素隐藏仍然占位
3. opacity
设置透明度,取值0(透明) ~ 1(不透明)
注意 :
1. rgba()设置某一个CSS属性为半透明;opacity设置元素整体的半透明,包含自身文本内容,背景样式和所有子元素
2. 父子元素同时设置opacity半透明,子元素最终的透明度是在父元素半透明基础上的再次半透明
例 :
父 : opacity:.5;
子 : opacity:.5;
子元素最终呈现为0.5*0.5的透明度
4. cursor
设置鼠标形状
取值 : 
default : 箭头
pointer : 手指
-----------
text    : 'I'
5. 列表样式
list-style:none; 取消列表的项目符号
了解 :
list-style-type : 设置项目符号类型
list-style-image : 自定义项目符号,取url()
list-style-position : 设置项目符号的位置
取outside(默认) / inside
默认项目符号显示在内容框的外部

*. 解决水平方向上由于代码换行导致的空隙
解决方式 :
1. 代码书写在一行
2. 父元素设置font-size:0;子元素调整字体大小为正常
3. 设置元素浮动

```



## JS

浏览器解释型语言，嵌套在HTML 文件中交给浏览器解释执行

作用：JS 用于实现用户交互，网页动态效果，或者游戏开发

组成：
核心语法： ECMAScript

内置对象： 

外置对象： BOM/DOM

JS使用

### 元素绑定事件

事件：所有用户的行为（鼠标，键盘操作）都是事件

语法：将事件函数作为标签属性绑定到元素上

例：单击事件：onclick

<button onclick="JS代码">hello</button>

JS语句：

alert("hello");网页弹幕

console.log("");

注意：涉及标签嵌套，采用外双内单的写法

### 文档内嵌

借助于<script type="text/javascript"></script>书写代码，标签内容即为JS语句

注意：脚本标签可以书写在文档的任意位置，书写任意多次，不同的书写位置代码执行的结果会有所不同，并且有可能阻塞代码运行

### 外链

创建外部的JS文件，以 .js 为后缀

在HTML 文件中借助 <script src=""></script>引入

注意：<script></script>可以内嵌JS 语句也可以引入JS文件，但是只能二选一，不能混用

#### href与src 的区别：

href ： 用于建立连接关系( <link href="">   <a href=""></a>) 不会礼嘛请求文件资源

src ： 用于设置 网页运行不可或缺的内容， 所以会直接请求src 的文件资源

#### JS输出语句

```javascript
console.log()  控制台输出
alert（） 	警告框
prompt("")  带有输入框的弹框
document.write(); 在body中写入内容，可识别标签语法
```

# Jquery



# flask



#  Django