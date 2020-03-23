# cookies

[TOC]



## 获取span 标签内的值 innerHTML

```php+HTML
<body>
    <span id='sp'>ACFP</span>
    <img src="pangyiliangpi.jpg" alt="" id="img">
    <button onclick='showInfo()'>识别span标签</button>

    <script type="text/javascript">
        function showInfo(){
            alert(sp.innerHTML);
        }
    </script>
</body>
```

