# 动态获取 select option 的自定义属性值

[TOC]







```javascript
var selectHtml = '';
for(var index in result.retData.detail){
    var subnet =  result['retData']['detail'][index]['subnet']+'/'+result['retData']['detail'][index]['mask'];
    var owner = result['retData']['detail'][index]['owner'];
    var uniqSubnetId = result['retData']['detail'][index]['uniqSubnetId'];
    selectHtml += '<option value="'+subnet+'" owner="'+ owner +'" uniqSubnetId="'+ uniqSubnetId +'">'+subnet+'</option>';
}
$('#add_lb_subnet_select').html(selectHtml);
```



```javascript
var obj=document.getElementById("add_lb_subnet_select");
var index=obj.selectedIndex;
var owner=obj.options[index].getAttribute("owner");
var uniqSubnetId=obj.options[index].getAttribute("uniqSubnetId");
```

