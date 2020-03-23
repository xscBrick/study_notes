# PHP 数组的多维转换（二维转三维，三维转二维）

前言：工作中经常会碰到数据的组装与拆解的问题，记录以便以后能够方便查阅

### 二维转三维

```php
$dataRes=array(
	[0]=>array(
    	[Id] => 15
        [uniqId] => f49l6u0z
        [owner] => 1251001049
        [updateTime] => 2019-08-04 16:47:20
            
    )
); //一个二维数组
$dataArr = array();
foreach ($dataRes as $k=>$v){
    $dataArr[$v['Id']][]= $v;
}
print_r($dataArr);
//返回
$dataArr=array(
	[15] => array(
        [0]=>array(
            [Id] => 15
            [uniqId] => f49l6u0z
            [owner] => 1251001049
            [updateTime] => 2019-08-04 16:47:20

        )
    )
);
```

### 三维转二维（降维）

```php
$dataArr=array(
	[0] => array(
        [0]=>array(
            [Id] => 15
            [uniqId] => f49l6u0z
            [owner] => 1251001049
            [updateTime] => 2019-08-04 16:47:20

        )
    ),
    [1] => array(
        [0]=>array(
            [Id] => 16
            [uniqId] => f49l6u0z444
            [owner] => 1251001049444
            [updateTime] => 2019-08-04 16:47:20

        )
    )
);//三维数组
array_walk($dataArr, function(&$v) {$v = current($v);});
print_r($dataArr);
//返回值
$dataArr=array(
	[0]=>array(
    	[Id] => 15
        [uniqId] => f49l6u0z
        [owner] => 1251001049
        [updateTime] => 2019-08-04 16:47:20
            
    )
); //一个二维数组
```

```php
$dataArr=array(
	[0] => array(
        [0]=>array(
            [Id] => 15
            [uniqId] => f49l6u0z
            [owner] => 1251001049
            [updateTime] => 2019-08-04 16:47:20

        )
    ),
    [1] => array(
        [0]=>array(
            [Id] => 16
            [uniqId] => f49l6u0z444
            [owner] => 1251001049444
            [updateTime] => 2019-08-04 16:47:20

        )
    )
);//三维数组
$newArr = array()
foreach ($dataArr as $k=>$v){
    $newArr[$v] = $v[0]
}
print($newArr);
    
    
```

