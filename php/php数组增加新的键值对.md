php数组增加新的键值对

> 加一个取地址符&

$result = array(

​	[detail] => Array
​        (
​            [0] => Array
​                (
​                    [name] => php
​                    [weight] => 10
​                    [region] => sz
​                    )
​		)

)

$Res = Array

(

​    [detail] => Array

​        (

​            [0] => Array

​                (

​                    [vbcId] => 3

​                    [vpcId] => 688

​                    [vbcInstanceId] => 10          

​                )））

```php
foreach ($Res['returnData']['detail'] as &$data){    
	foreach ($result['returnData']['detail'] as $row){        
		if ($data['regionId'] == $row['regionId']){            
			$data['vbcgwId'] = $row['vbcgwId'];            
			$data['uniqVbcgwId'] = $row['uniqVbcgwId'];            
			$data['gwIp'] = $row['instance'][0]['gwIp'];        
			}    
	foreach ($resultInstanceNum['returnData']['detail'] as $num){        
		if ($data['vbcId'] == $num['vbcId']){            
			$data['vbcInstanceNum'] = $num['vbcInstanceNum'];            
			$data['lastUpdateStateTime'] = $num['lastUpdateStateTime'];        
			}    
		}    
	}
}
```

在$data 前加一个取地址符&