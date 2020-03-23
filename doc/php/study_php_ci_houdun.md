# study_php_ci_wangdun

[TOC]

## 新建一个控制器

新建html文档：

html:xt + tab



## 默认控制器配置

config -> routes

```php
$route['default_controller'] = 'home';
```

home控制器

```php
<?php defined('BASEPATH') OR exit('no direct script access allowed');
class Home extends CI_Controller {
    public function index(){
        echo 'hello world';
        $this->load->view('home');
    }

}
```

view_home

```php
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
    <title>Document</title>
</head>
<body>
<hr>
这是一个home文件
</body>
</html>

```

![image-20191110001047289](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191110001047289.png)

## 载入多个视图

```php
$this->load->view('index/head');
$this->load->view('index/home');
$this->load->view('index/home.html');
$this->load->view('index/foot');
```



## 载入辅助函数：helper()

### 前提：载入url函数

```php
$this->load->helper('url');//application/config.autoload.php；里设置$autoload['helper'] = array('url');自动加载
redriect('home/test');
echo site_url();//获得url参数段路径：http://127.0.0.1/CI/index.php
echo '<br/>';
echo base_url();//获得根路径： http://127.0.0.1/CI/
redirect();//跳转
```

## 自动载入

```php
//config->autoload.php
$autoload['helper'] = array('url');
redirect('控制器名/方法名');//跳转
```

## 自定义全局函数

system->core->Common.php

```php
function p($arr){
    echo '<pre>';
    print_r($arr) ;
    echo '</pre>';

}
//controller
p($data);
```



## 表单验证

```php
//载入验证类
$this->load->library('form_validation');
//设置规则
$this->form_validation->set_rules('name值','标签名称','规则')
//执行验证(返回bool值)
$this->form_vildation->run()
```



### 表单验证辅助函数

```php
$this->load->helper('form');
set_vlaue('name') //重填数据
form_error('name','<span>', '</span>') //显示错误
set_select()
set_checkbox()
set_redio()

```

tr>td*2 ->tab

###  载入模板

