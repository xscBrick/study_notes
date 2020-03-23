# foreach 循环嵌套数组优化

```php


        $vpnArr = $this->Tvpc_oss_model->getVpcInfoDetail($this->_post);

        $ipv6Arr = $this->Tvpc_oss_model->getVpcIPv6Info($this->_post);

        if(is_array($vpnArr) && $vpnArr['returnValue'] == 0){
            if(is_array($ipv6Arr) && $ipv6Arr['returnValue'] == 0){


                $newArr = array();
                foreach ($ipv6Arr['returnData']['detail'] as $key=>$val){
                    $newArr[$val['uniqVpcId']] = $val;
                }
                foreach ($vpnArr['returnData']['detail'] as $k=>&$v){
                    if(isset($newArr[$v['uniqVpcId']])){
                        $v['address'] = $newArr[$v['uniqVpcId']]['address'];
                    }else{
                        $v['address'] = '无';
                    }
                }
                unset($newArr);
                exit($this->output->succ($vpnArr['returnData']));
            }else{
                exit($this->output->result(-1, array(), '获取IPv6地址段失败'));
            }
    	}else{
    		exit($this->output->result(9017, array(), 'get vpcInfo fail'));
    	}
	}
```

### 降维

```php
array_walk($modifyArr, function(&$v) {$v = current($v);});
```

![1564916778905](C:\Users\v_xscxu\AppData\Roaming\Typora\typora-user-images\1564916778905.png)

![1564916784870](C:\Users\v_xscxu\AppData\Roaming\Typora\typora-user-images\1564916784870.png)