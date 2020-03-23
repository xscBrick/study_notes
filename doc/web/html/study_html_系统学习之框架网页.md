# study_html_系统学习之框架网页

[TOC]

## 框架

如果我们要实现 框架网页，就需要将 frameset 标签取代 body 标签

framset 	标签框架集

如何将一个浏览器



### frameset 标签 cols rows

frameset 原始可定义一个框架集，它被用来组织多个窗口，每个群框架存有独立的文档，在其最简单的应用中， frameset 元素仅仅会规定在框架集存在多少行，多少列，必须使用cols rows(水平分隔) 苏醒

```
<!-- 
    如果我们要实现 框架网页就需要将 frameset标签取代 body 标签
    将一个浏览器窗口分隔为 100 像素的高，其他的高应该都给下窗口

    frame 不能分隔，只能表示小窗口
 -->
<frameset rows="100,*" scrolling="auto">
    <!-- 表示上窗口 -->
    <frame noresize>
        <!-- -->
        <frameset cols="100,*">
            <!-- 左边小窗口 -->
            <frame />
            <!-- 右边窗口 -->
            <frame />
        </frameset>
</frameset>
```



#### frameset 属性

```
noresize //不能调整 框架的大小，属性无值
frameborder	0|1 规定是否显示框架周围的边框
cols 	垂直分隔
rows	水平分隔
```



#### 标准属性 id class title style



### frame 不能分隔

frame 这个标签不能分隔，只能表示小窗口，只有 frameset 标签才可以分隔



#### frame 属性

```
noresize //不能调整 框架的大小，属性无值
frameborder	0|1 规定是否显示框架周围的边框
src	规定在框架中显示的文档的url
scrolling	yes|no|auto	规定是否在框架中显示滚动条
name 	规定框架的名称
```



## iframe 浮动框架

可以放在body 标签下

给html 挖坑 用于展示 小窗口

```
<iframe width="100%" height="600" src="http://www.baidu.com" frameborder="0" name="iframe"></iframe>
    <br>
    <a href="http://www.tencent.com" target="iframe">跳转到腾讯</a>
    <br>
    <a href="http://www.baidu.com" target="iframe">跳转到百度</a>
```

