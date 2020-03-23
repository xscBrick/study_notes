JS 碎片笔记

> **JS 区分大小写,对大小写敏感**

> JavaScript 函数是将语句组合在块中的典型例子

```javascript
function myFunction()
{
document.getElementById("demo").innerHTML="Hello World";
document.getElementById("myDIV").innerHTML="How are you?";
}
```

>  **变量是存储信息的容器。**

```javascript
var pi=3.14;
var name="Bill Gates";
```

*如果重新声明 JavaScript 变量，该变量的值不会丢失*

> 声明变量类型 使用关键词 'new'

```javascript
var x = new String;
//创建一个新的对象也可以用关键词 “new”
person = new Object();
person.name = "baobao";
person.age = 3;
```

>  **JavaScript 函数:**函数是由事件驱动的，或者当它被调用时可重复执行的代码块



> 条件运算符（类似于三目运算符）
> variablename=(condition)?value1:value2 

```javascript
variablename=(condition)?value1:value2 
//如果变量 visitor 中的值是 "PRES"，则向变量 greeting 赋值 "Dear President "，否则赋值 "Dear"。
```

> If...else if...else 语句

> **switch break  default**

工作原理：首先设置表达式 n（通常是一个变量）。随后表达式的值会与结构中的每个 case 的值做比较。如果存在匹配，则与该 case 关联的代码块会被执行。
请使用 **break** 来阻止代码自动地向下一个 case 运行。
**default** 关键词来规定匹配不存在时做的事情：

```javascript
var day=new Date().getDay();
switch (day)
{
case 6:
  x="Today it's Saturday";
  break;
case 0:
  x="Today it's Sunday";
  break;
default:
  x="Looking forward to the Weekend";
}
```

## 不同类型的循环

JavaScript 支持不同类型的循环：

- *for* - 循环代码块一定的次数  
- *for/in* - 循环遍历对象的属性  
- *while* - 当指定的条件为 true 时循环指定的代码块  
- *do/while* - 同样当指定的条件为 true 时循环指定的代码块 

```javascript
for (var i=0; i<5; i++)
  {
  x=x + "The number is " + i + "<br>";
  }
```

其他写法：

```javascript
var i=0,len=5;
for (; i<len; )
{
document.write("The number is " + i + "<br>");
i++;
}
```

### 异常 try catch throw

```javascript
<script>
    function myFunction()
    {
        try
          {
          var x=document.getElementById("demo").value;
          if(x=="")    throw "empty";
          if(isNaN(x)) throw "not a number";
          if(x>10)     throw "too high";
          if(x<5)      throw "too low";
          }
        catch(err)
          {
          var y=document.getElementById("mess");
          y.innerHTML="Error: " + err + ".";
      }
}
</script>

<h1>My First JavaScript</h1>
<p>Please input a number between 5 and 10:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="mess"></p>
```

请注意，如果 getElementById 函数出错，上面的例子也会抛出一个错误。

### onclick onload onunload onchange 

>  onclick 事件会在点击的时候触发

```javascript
<h1 onclick="this.innerHTML='谢谢!'">请点击该文本</h1>
<button onclick="displayDate()">点击这里</button>
document.getElementById("myBtn").onclick=function(){displayDate()};

```



>  onload 和 onunload 事件会在用户进入或离开页面时被触发onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。
> onload 和 onunload 事件可用于处理 cookie。

```javascript
<body onload="checkCookies()">
    
```

### onchange 事件常结合对输入字段的验证来使用。

```javascript
<input type="text" id="fname" onchange="upperCase()">
//当用户改变输入字段的内容时，会调用 upperCase() 函数
```

### onmouseover 和 onmouseout 事件

*onmouseover 和 onmouseout 事件可用于在用户的鼠标移至 HTML 元素上方或移出元素时触发函数。*

### onmousedown、onmouseup 以及 onclick 事件

onmousedown, onmouseup 以及 onclick 构成了鼠标点击事件的所有部分。首先当点击鼠标按钮时，会触发 onmousedown  事件，当释放鼠标按钮时，会触发 onmouseup 事件，最后，当完成鼠标点击时，会触发 onclick 事件。

### 删除已有的 HTML 元素

如需删除 HTML 元素，您必须首先获得该元素的父元素：

```javascript
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>
```

**提示：**如果能够在不引用父元素的情况下删除某个元素，就太好了。

不过很遗憾。DOM 需要清楚您需要删除的元素，以及它的父元素。

这是常用的解决方案：找到您希望删除的子元素，然后使用其 parentNode 属性来找到父元素：

```javascript
var child=document.getElementById("p1");
child.parentNode.removeChild(child);
```

## HTML DOM 

- 如何改变 HTML 元素的内容 (innerHTML)  
- 如何改变 HTML 元素的样式 (CSS)  
- 如何对 HTML DOM 事件作出反应  
- 如何添加或删除 HTML 元素

```javascript
div id="div1">
<p id="p1">这是一个段落</p>
<p id="p2">这是另一个段落</p>
</div>

//添加HTML元素
<script>
var para=document.createElement("p");				//创建一个<p>元素
var node=document.createTextNode("这是新段落。");  	//创建文本节点
para.appendChild(node);								//向 <p> 元素追加这个文本节点

var element=document.getElementById("div1");		//找到一个已有的元素
element.appendChild(para);							//向一个已有的元素追加这个新元素
</script>

//删除HTML元素
<script>
var parent=document.getElementById("div1");	//找到父元素
var child=document.getElementById("p1");	//找到要删除的<p>元素
parent.removeChild(child);					//删除<p>元素
</script>

```