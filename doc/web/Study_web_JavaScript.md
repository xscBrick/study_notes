# Study_web_JavaScript

[TOC]

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



## JSON.parse(), JSON.stringfy();

 JSON对象的两个方法：JSON.parse()和JSON.stringify()通常用作JSON对象和字符串之间的相互转换  JSON.parse(string)：接受一个JSON字符串并将其转化成一个JavaScript对象。
JSON.stringify(obj)：接受一个JavaScript对象并将其转化为一个JSON对象。 

```javascript
var a = {'name':'tom','sex':'男','age':'24'};//json对象
var b = '{"name":"Mike","sex":"女","age":"29"}';//json字符串，注意是字符串
var aToStr = JSON.stringify(a);//JSON.stringify()是把json对象转化为字符串
var bToObj = JSON.parse(b);//JSON.parse是把字符串转化为json对象
console.log(typeof(aToStr)); //stringify
console.log(typeof(bToObj)); //object

const myArr = ['bacon', 'letuce', 'tomatoes'];
const myArrStr = JSON.stringify(myArr);
console.log(myArrStr);
console.log(JSON.parse(myArrStr));
```



```
JSON.parse(text[, reviver])
```

- **text:**必需， 一个有效的 JSON 字符串。
- **reviver:** 可选，一个转换结果的函数， 将为对象的每个成员调用此函数。

```javascript
<p id="demo"></p>
<script>
var obj = JSON.parse('{ "name":jb51", "alexa":10000, "site":<a href="//www.jb51.net">www.jb51.net</a> }');
document.getElementById("demo").innerHTML = obj.name + "：" + obj.site;
</script>
```

首先通过parse()方法将JSON数据转换为JavaScript对象，

解析完成后，我们就可以在网页上使用JSON数据了

```javascript
JSON.parse('{"p": 5}', function(k, v) {
  if (k === '') { return v; } 
  return v * 2;               
});                          
 
JSON.parse('{"1": 1, "2": 2, "3": {"4": 4, "5": {"6": 6}}}', function(k, v) {
  console.log(k); // 输出当前属性，最后一个为 ""
  return v;       // 返回修改的值
});
```

```javascript

```



[TOC]