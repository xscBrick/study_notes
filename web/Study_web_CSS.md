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

```html
<link rel="stylesheet" href="URL" type="text/css">
```

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
1. content-box
默认值,除表单元素外,大多采用默认的计算方式
元素最终在文档中的尺寸由盒模型属性值依次相加得到
width/height设置的尺寸对应为元素内容框的大小
2. border-box
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

