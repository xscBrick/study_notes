# Study_PHP_CI

[TOC]

## 一.CI的HelloWorld！

注意：CI禁止直接通过文件目录来访问控制器。

 ./application/controllers/hello.php
 1 <?php 2 //放止用户直接通过路径来访问控制器，如果这样的话会显示找不到（封装）
 3 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 4 
 5 class Hello extends CI_Controller {
 6 
 7     public function sayhello($name,$name2){
 8         echo $name,",Hello CI to ",$name2;
 9     }
10 }



## 二.CI的文本计时器demo——文本操作与调用视图操作

调用视图的基本格式：

$this->load->view('XXX');

 

 1 <?php
 2 //./applications/controllers/hello.php
 3 //放止用户直接通过路径来访问控制器，如果这样的话会显示找不到（封装）
 4 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 5 
 6 class Hello extends CI_Controller {
 7 
 8     public function sayhello($name,$name2){
 9         echo $name,",Hello CI to ",$name2;
10     }
11 
12     public function show(){
13         $name = "deng";
14         @$count = file_get_contents('./num.txt');  //装饰器
15         $count = $count ? $count:0;
16         $count++;
17         $data = array('key'=>$name,'value'=>$count);
18 
19         $re = fopen('./num.txt','w');
20         fwrite($re, $count);
21 
22         $this->load->view("testview.php",$data);   //装载两个视图页面
23         $this->load->view("testview2.php");
24     }
25 }



## 三.CI的数据库demo——对数据模型的增，删，改，查

### 数据模型——

#### 1.数据模型是一个数据库类

#### 2.一个模型针对一张表

创建一个模型必须注意——

必须继承数据核心类CI_Model，同时重载父类中的构造方法

class Model_name extends CI_Model
{
function __construct()
    {
        parent::__construct();
    }
}

### 对数据库的操作——

#### 1.连接数据库（$this->load->database());

#### 2.插入数据（$this->db->insert($t_name,$arr);)

$t_name——你要操作的表]

$arr——你要插入的数据("key"=>value)

#### 3.更新数据

$this->db->where(字段名，字段值)

$this->db->update(表名，修改值的数组)

#### 4.查询数据

$this->db->where(字段名，字段值)

$this->db->select(字段)

$query = $this->db->get(表名)

return $query->result();

#### 5.删除数据

$this->db->where(字段名，字段值)

$this->db->delete(表名)

 

 1 ./application/controllers/user.php
 2 <?php 
 3 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 4 
 5 class User extends CI_Controller {
 6 
 7     public function insert(){
 8         $this->load->model('test_m');
 9         $arr = array('usid'=>1,'uname'=>'deng1','upass'=>'1234');
10         $this->test_m->user_insert($arr);
11     }
12 
13     public function update(){
14         $this->load->model('test_m');
15         $arr = array('usid'=>22,'uname'=>'deng222','upass'=>'1233333');
16         $this->test_m->user_update(2,$arr);
17     }
18 
19     public function delete(){
20         $this->load->model('test_m');
21         $this->test_m->user_delete(22);
22     }
23 
24     public function select()
25     {
26         $this->load->model('test_m');
27         $arr = $this->test_m->user_select(1);
28         print_r($arr);
29         echo $arr[0]->usid;
30 
31     }
32 }
33 
34 /* End of file welcome.php */
35 /* Location: ./application/controllers/welcome.php */


 1 <?php
 2 /**
 3 *  ./application/models/test_m.php
 4 */
 5 class Test_m extends CI_Model
 6 {
 7     
 8     function __construct()
 9     {
10         parent::__construct();
11         //connect to the database
12         $this->load->database();
13         //$this->load->insert($t_name,$data)
14     }
15 
16     function user_insert($arr){
17         $this->db->insert('user',$arr);
18     }
19 
20     function user_update($id,$arr)
21     {
22         $this->db->where('usid',$id);
23         $this->db->update('user',$arr);
24     }
25 
26     function user_delete($id){
27         $this->db->where('usid',$id);
28         $this->db->delete('user');
29     }
30 
31     function user_select($id){
32         $this->db->where('usid',$id);
33         $this->db->select('*');
34         $query = $this->db->get('user');
35         return  $query->result();
36     }
37 }
38 ?>

##  四.CI的文件上传demo

###  1.面向过程的文件上传方法

 

 1 #/controllers/upload.php
 2 <?php 
 3 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 4 
 5 class Upload extends CI_Controller {
 6 
 7     //显示带表单的视图
 8     public function index(){
 9         $this->load->view('up');
10 
11     }
12 
13     //显示上传信息
14     public function up(){
15 
16         if(!empty($_POST['sub'])){
17             //打印变量的函数
18             //var_dump($_FILES['upfile']);   
19             $file = $_FILES['upfile'];
20             if($file['size'] >= 20000000){
21                 echo "size no!";
22             }
23             else{
24                 switch ($file['type']) {
25                     case 'image/jpeg':
26                         $br = '.jpg';
27                         break;
28                     
29                     default:
30                         $br = false;
31                         break;
32                 }
33 
34                 if($br){
35                     $time = time();
36                     move_uploaded_file($file['tmp_name'], "./upload/$time$br");
37 
38                 }
39                 else{
40                     echo "type no";
41                 }
42             }
43 
44         }
45     }
46 
47 }

1 #/views/up.php

2 <html>
3 <!--注意相对路径的建立-->
4     <form action="/CI/index.php/upload/up" method="post" enctype="multipart/form-data">
5         <input type="file" name="upfile" />
6         <input type="submit" name="sub" value="提交" />
7     
8     </form>
9 </html>

###  2.面向对象的CI框架文件上传方法

 

####  a.定义一个数组，设置一些与上传相关的参数

//设置上传目录，这里写./,目录要建在网站根目录，就是和application同级

//如果你要放在application目录下，可以用系统定义的路径常量APPPATH

//例如：APPPATH.'uploads/'

$config['upload_path'] = './uploads/';

//设置允许上传的类型

$config['allowed_types'] = 'gif|jpg|png';

$config['max_size'] = '100';

//如果是图片还可以设置最大高度和宽度

$config['max_height'] = 768;

$config['max_width'] = 1024;

#### b.还可以设置其他的一些额外参数，详细看用户手册

#### c.调用CI的上传通用类，并执行上传

//upload为调用的类名，全小写

$this->load->library('upload',$config);

//如果上传框的name写的是userfile，那就不用传参数了，如果不是，把name的值传进去

$this->upload->do_upload('上传框的name');

#### d.接收出错信息或成功信息

//出错信息

$error = array('error' => $this->upload->display_error());

//成功信息

$data = array('upload_data' => $this->upload->data());

 

 1 <?php 
 2 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 3 
 4 class Upload extends CI_Controller {
 5 
 6     //显示带表单的视图
 7     public function index(){
 8         $this->load->view('up');
 9 
10     }
11 
12     //显示上传信息
13     public function up(){
14 
15         $config['upload_path'] = './uploads/';
16         $config['allowed_types'] = 'gif|jpg|png';
17         $config['max_size'] = "2000";
18 
19         $this->load->library('upload',$config);
20 
21         //打印成功或错误的信息
22         if($this->upload->do_upload('upfile'))
23         {
24             $data = array("upload_data" => $this->upload->data());
25             var_dump($data);
26         }
27         else
28         {
29             $error = array("error" => $this->upload->display_errors());
30             var_dump($error);
31         }
32     }
33 
34 }

##  五.CI的登录验证demo

### 1.利用CI类实现session登录

#### a.修改配置文件（config.php）

$config['encryption_key']

#### b.加载SESSION类

$this->load->library('session');

#### c.创建SESSION

$this->session->set_userdata($array);

#### d.查看SESSION

$this->session->userdata(session名);

#### e.删除SESSION

$this->session->unset_userdata('SESSION名');

 

 1 ./application/controllers/login.php
 2 <?php 
 3 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 4 
 5 class Login extends CI_Controller {
 6 
 7     public function index()
 8     {
 9         $this->load->view('login.html');
10     }
11 
12     public function checklogin(){
13         $this->load->model("test_m");
14         $user = $this->test_m->user_select($_POST['uname']);
15         if($user){
16             if($user[0]->upass == $_POST['upass']){
17                 echo '密码正确！';
18                 $this->load->library('session');
19                 $arr = array("uid" => $user[0]->usid);
20                 $this->session->set_userdata($arr);
21                 echo "<br />";
22                 echo $this->session->userdata('uid');
23             }
24             else{
25                 echo '密码不正确！';
26             }
27         }
28         else{
29             echo '用户名不存在';
30         }
31     }
32 
33     public function checksession(){
34         $this->load->library('session');
35         if($this->session->userdata('uid')){
36             echo '已经登录。';
37         }
38         else{
39             echo '没有登录。';
40         }
41     }
42 
43     public function loginout(){
44         $this->load->library('session');
45         $this->session->unset_userdata('uid');
46     }
47 }

##  六.CI的分页功能demo

### 1.必须知道的一些参数

a.总共有多少条记录

b.一页要有多少条记录

c.总共多少页

d.当前页前后要显示多少个分页链接

### 2.设置一些CI分页类基本参数

//总条数

$config['total_rows']

//一页显示几条

$config['per_page']

//定义当前页的前后各有几个数字链接

$config['num_links']

//定义没有分页参数,主URL

$config['base_url']

### 3.调用CI的分页类

$this->load->library('pagination');

4.执行分页方法

$this->pagination->initialize($config);

### 5.输出分页链接

echo $this->pagination->create_links();

### 6.查询部分数据(limit)

echo $this->db->limit($num,$start);  //从$start查$num条

 1 ./applications/controllers/page.php
 2 <?php 
 3 if ( ! defined('BASEPATH')) exit('No direct script access allowed');
 4 
 5 class Page extends CI_Controller {
 6 
 7     public function user_add(){
 8         $this->load->model('test_m');
 9 
10         for ($i = 1;$i <= 100;$i++){
11             $name = 'u'.$i;
12             $arr = array("usid"=>$i,"uname"=>$name,"upass"=>123456);
13             $this->test_m->user_insert($arr);
14 
15         }
16     }
17 
18     public function pagelist(){
19         $this->load->model('test_m');
20         $user = $this->test_m->user_select_all();
21         $allnum = count($user);
22         $pagenum = 20;
23 
24         $config['total_rows'] = $allnum;
25         $config['per_page'] = $pagenum;
26         $config['num_links'] = 3;
27         $config['base_url'] = "/CI/index.php/page/pagelist";
28         $config['use_page_numbers'] = true;
29 
30         $this->load->library('pagination');
31         $this->pagination->initialize($config);
32 
33         var_dump($this->pagination->create_links());
34         echo $this->pagination->create_links();
35 
36         echo "<br />";
37         $id = $this->uri->segment(3);  //获得url第三段字符
38         $id =$id ? $id:1;
39         $start = ($id - 1) * $pagenum;
40         $list = $this->test_m->user_select_limit($start,$pagenum);
41         var_dump($list);
42     }
43 }

## <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

防止访问不是从index 过来的,防止跨站攻击，直接通过访问文件路径用的

##  APPPATH 和 BASEPATH

其中 APPPATH 是相对路径（application目录路径），而BASEPATH是绝对路径（system目录的路径）

[

```html
https://www.626x.com/tag/%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98%E8%B5%84%E6%BA%90%E5%8C%85/
```

](https://www.626x.com/tag/百度网盘资源包/)