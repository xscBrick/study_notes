# Study_PHP_curl

  在html中，我们可以通过form设置http的post和get提交，但假如我们获取的数据不是从html中来的，而是php脚本主动向其他服务器提交呢？这个时候，我们应该怎么实现post和get提交数据呢？答案就是php的curl函数或者stream_context_create函数，还有fsockopen函数等等方式，这里讲一下curl的提交设置，其他两种有时间会写一下。

　　curl的函数实现http提交，关键就在四个函数：

　　　　一个是：curl_init()

　　　　作用：初始化curl的``套接流``

　　　　第二个是：curl_setopt()

　　　　作用：设置http提交参数

　　　　第三个是:curl_exec()

　　　　作用：执行curl ``套接流`` 的提交，并获取服务器返回的内容

　　　　第四个：curl_close()

　　　　作用：关闭已经实现http提交目的的``套接流``

　　　　说是说四个函数，但实际的应用中，其实，就是设置curl_setopt这个函数的参数而已，其他三个都是跑龙套的，呵呵。

　　　　不相信，下面我们举一个例子来利用curl系列函数实现http提交，不罗嗦了，直接上代码：  

```php
<?php
/*
*创建一个curl_init提交函数，模拟get提交，模拟post提交，模拟json提交
*$url 提交的服务器地址，必须
*$data 提交的数据，必须，是关联数组，
*$method 提交的方式，必须，默认get提交，选项值，只能填get、post、json
*$options 其他选项，可有可以无，如果设置了，不能设置CURLOPT_URL,必须符合curl_setopt_array()的参数语法
*如果失败则返回false，提交数据成功，则返回服务器返回的结果
*/
function curl($url='',$data=array(),$method='get',$options=array()){
    //验证数据传进来的数据是否合法
    if(empty($url) || !filter_var($url,FILTER_VALIDATE_URL)){
        return false;
    }
    if(!is_array($data) && empty($data)){
        return false;
    }
    $method = strtolower($method);
    if(!in_array($method,array('get','post','json'))){
        return false;
    }
    //初始化curl句柄，
    $ch = curl_init();
    //设置服务器返回的数据不直接输出，而是保留在curl_exec()的返回值中
    curl_setopt ($ch, CURLOPT_RETURNTRANSFER, 1);
    if(!empty($options) && is_array($options)){
        if(curl_setopt_array($ch,$options) == false){
            return false;
        }
    }
    switch($method){
        case 'get':
            //把要提交的数据转换为get键值对提交
            $data = http_build_query($data);
            curl_setopt($ch,CURLOPT_URL,$url.'?'.$data);
            //获取curl执行后，服务器返回的结果
            $return = curl_exec($ch);
            curl_close($ch);
            return $return;
            break;
        case 'post':
            curl_setopt($ch,CURLOPT_URL,$url);
            //设置post提交
            curl_setopt($ch,CURLOPT_POST,true);
            //提交post的数据
            curl_setopt($ch,CURLOPT_POSTFIELDS,$data);
            $return = curl_exec($ch);
            curl_close($ch);
            return $return;
            break;
        case 'json':
            //设置json提交的数据
            $data = json_encode($data);
            curl_setopt($ch,CURLOPT_URL,$url);
            //设置post提交
            curl_setopt($ch,CURLOPT_POST,true);
            //json的数据通过post的方式提交
            curl_setopt($ch,CURLOPT_POSTFIELDS,$data);
            $return = curl_exec($ch);
            curl_close($ch);
            return $return;
            break;
        default:
            return false;
        break;
    }
}
 $url = "http://www.test.com/curl_setopt/upload.php";
 //下面是测试，本人是测试成功了，我服务器是直接输出$_POST，$_GET
 $data  = array( 'name'  =>  'curl' , 'method' => 'post' );
 $method ='post';
 var_dump(curl($url,$data,$method));
```

