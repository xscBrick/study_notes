# Study_PHP

[TOC]

## 引用传递

### 形参与实参

形参：不具有实际意义，在函数定义的时候创建

实参：具有实际数据意义的参数，事在函数调用时使用的参数

联系：形参时实参的载体，实参在调用时通常是需要传入到函数内部参与计算（运算），那么需要在函数内部去找到实际数据所在的位置才能找到数据本身：需要实际调用的时候，将数据以实参的形式传递给形参：给形参赋值，从而使得函数内部可以用到外部数据。

实参  >= 形参

默认值：函数在定义时，给形参进行一个初始赋值（默认值的定义时放在最右边的（多个））

```php
function defaultValue($num1 = 1, $num2 = 2){
	echo $num1 + $num2
}
defaultValue(3) //5
```

实参子啊调用时，会将值赋值给形参，实际上是一个简单的值传递，有的时候希望在函数内部拿到外部数据，能够在函数内部改变，那么就需要明确告知函数（定义时），函数才会在调用时去主动获取外部数据的内存地址，以上这种定义形式参数的方式叫做引用传值

```php
$a = 10;$b = 5;
function display($a, &$b){
$a = $a * $a;
$b = $b * $b;
echo $a, '<br/>', $b, '<br/>';
}
display($a, $b)	//100,25
echo '<hr/>', $a, '<br/>', $b; //10,25
```

### 静态变量 static

跨函数共享数据（同一个函数被多次调用）

作用：当前函数被调用的次数，统筹函数多次调用得到的不同结果

## 常量 const

常量前没有 $ 

常量只能用 define()函数定义,不能通过赋值语句

常量不用理会变量的作用域,在任何地定义和访问

常量一旦定义就不能被重新定义或取消定义

常量的值只能是标量

```php
//定义常量1
<?php
    define("CONSTANT", "hello world.");
	echo CONSTANT;	//hello world
?>
//定义常量2
const PI = 3.14;
```



### 匿名函数

没有名字的函数

```php
$fun = function(){
	echo('hello world')
}
```

## 闭包 closure

函数内部有一些局部变量在函数执行之后没有被释放，是因为在函数内部还有对应的函数在引用

## 时间函数

```php
echo date('Y 年 m 月 d 日 H:i:s', 12345678), '<br/>'
echo time()		//获取当前时间对应的时间戳
echo microtime() 	//微妙级别的时间
```

```php
<?php
echo '当前时间戳:', time();
echo '<br/>';
echo '当前时间是:', date('Y 年 m 月 d 日 H:i:s', time());
echo '<br/>';
echo '今天是', date('m 月第 d 天 l', time())
?>
```



## 有关数学的函数

max()：指定参数中最大的值
min()：比较两个数中较小的值
rand()：得到一个随机数，指定区间的随机整数
mt_rand()：与rand一样，只是底层结构不一样，效率比rand高（建议使用）
round()：四舍五入
ceil()：向上取整
floor()：向下取整
pow()：求指定数字的指定指数次结果：pow(2,8) == 2^8 == 256
abs()：绝对值
sqrt()：求平方根

## 文件包含四种形式

include： 包含文件,包含不到文件时,错误级别较轻,不会阻止代码的执行

include_once:最多被包含一次

Require：与include相同, 包含不到文件时,错误级别较高,有保温错误代码,不再执行

Require_once:与include_once相同

include 'filename';

include('文件名字'); 	//文件名字:路径问题

## 作用域

> 全局: 用户普通定义的变量
>
> 局部: 函数背部定义的变量
>
> 超全局: 系统定义的变量 .
> 	访问全局变量：但是必须使用数组方式
>
> ```php
> $_SERVER, $_POST, $GLOBALS
> $global = 'global area';
> $GLOBALS['global'];	//global area
> ```

## 字符串类型

单引号,双引号 字符串

没有单引号的单引号字符串 nowdoc

```php
//nowdoc 结构
$str = <<<'EOD'
	hello
EOD;
var_dump($str); //string(7) "hello"
```

没有双引号的双引号字符串 heredoc 接口

```php
//heredoc 结构
$str = <<<EOD
	hello
EOD;
var_dump($str); //string(7) "hello"
```

### 字符串转义

在PHP中系统常用的转义符号：

\’：在单引号字符串中显示单引号

\”：在双引号字符串中显示双引号

\r：代表回车（理论上是回到当前行的首位置）

\n：代表新一行

\t：类似tab键，输出4个空格

\$：在PHP中使用$符号作为变量符号，因此需要特定识别

单引号和双引号的区别：

1、  其中单引号中能够识别\’，而双引号中就不能识别\’（下图浏览器查看的是页面源代码）

2、  双引号中因为能够识别$符号，所以双引号中可以解析变量，而单引号不可以

### 变量专业标识符（区分），给变量加上一组大括号{}

```php
$a = 'hello';
$str = "abc{$a}def"
echo $str;
```

## 字符串长度 函数 strlen()

```php
$str1 = 'abcdefg';
echo strlen($str1);//7
```

## 字符串相关函数

### 1.转换函数 implode, explode, str_split

#### implode(连接方式,数组)

将数组中的元素按照某个规则连接成一个字符串

#### explode(分割字符,目标字符串)

将字符串按照某个格式进行分割,变成数组

#### str_split(字符串,字符长度)

按照指定长度拆分字符串得到数组

### 2.截取函数: trim(), ltrim(), rtrim()

#### trim(字符串[, 指定字符])

trim()函数本身默认是用来去除字符串两边的空格(中间不行),但是也可以指定要去除的内容, 是按照指定的内容循环去除两边有的内容:直到碰到一个不是目标字符为止

```php
$str = ' abc d e f   ';
var_dump(trim($str)); //string(9) 'abc d e f'
```

### 3.截取函数: substr(), strstr()

#### substr(字符串,起始位置,长度)

指定位置开始截取字符串, 可以截取指定长度

#### strstr(字符串, 匹配字符)

从指定位置开始,截取到最后(可以用来去文件后缀名)echo

```php
$str = ' abc d e f   ';
echo substr($str, 1, 4);//abc 
echo strstr($str, 'c');	//c d e f
```

### 4.大小 转换: strtolower, strtoupper(),ucfist()

strtolower：全部小写(原字符串头尾空格会被去掉)

strtoupper：全部大写

ucirst：首字母大写

```php
$str = ' abc d e f   ';
echo stroupper($str), '<br/>';//ABC D E F
```

### 5.查找函数：strpos(), strrpos()

strpos(字符串，匹配字符)：判断字符在目标字符串中出现的位置（首次）

strrpos(字符串，匹配字符)：判断字符在目标字符串中最后出现的位置

### 6.替换函数：str_replace()

str_replace(匹配目标,替换的内容,字符串本身)

```php
$s = '123a234a345abcdef'
echo str_replace('a', 'b', $s);		//123b234b345bbcdef
```

### 7.格式化函数：printf(), sprintf()

printf/sprintf(输出字符串有占位符,顺序占位内容..)：格式化输出数据

```php
$a = 1;
$b = 2;
echo sprintf("%d + %d = %d", $a, $b, $a+$b); //1+2=3
```

### 8.其他: str_repeat(), str_shuffle()

str_repeat($str, n): 重复某个字符串n次

 str_shuffle($str): 随机打乱字符串

## 数组相关

- [ ] | 函数            | 作用                                 | 参数说明                                                     |
  | --------------- | ------------------------------------ | ------------------------------------------------------------ |
  | 1)排序函数      |                                      |                                                              |
  | sort($arr)      | 顺序排序(下标重排)                   | sort(array(3,1,2,5,0)) //0,1,2,3,5                           |
  | rsort($arr)     | 降序排序                             |                                                              |
  | asort($arr)     | 顺序排序(下标保留)                   |                                                              |
  | arsort()        | 逆序排序                             |                                                              |
  | ksort()         | 顺序排序(按照键名)                   |                                                              |
  | krsort()        |                                      |                                                              |
  | shuffle()       | 随机打乱数组元素，数组下标会重排     |                                                              |
  | 2)指针函数      |                                      |                                                              |
  | reset()         | 重置指针,将数组指针回到首位          | $arr = array(3,1,2,5,0);<br />echo reset($arr); //3<br />echo next($arr); //1<br />echo prev($arr); //3<br />echo end($arr); //0 |
  | end()           | 重置指针，将数组指针指导最后一个元素 |                                                              |
  | next()          | 指针下移                             | next和prev会移动指针，有可能导致指针移动到最前或者最后（离开数组），导致数组不能使用，通过next和prev不能回到真确的指针位置。只能通过end或者reset进行指针重置 |
  | prev()          | 指针上移                             |                                                              |
  | current()       | 获取当前指针对应的元素值             | echo current($arr); //3                                      |
  | key()           | 获取当前指针对应的下标值             | echo key($arr); //0                                          |
  | 3）其他函数     |                                      |                                                              |
  | count()         | 统计数组中元素的数量                 |                                                              |
  | array_push()    | 往数组中加入一个元素（数组后面）     |                                                              |
  | array_pop()     | 从数组中取出一个元素（数组后面）     |                                                              |
  | array_shift()   | 从数组中取出一个元素（数组前面）     |                                                              |
  | array_unshift() | 从数组中加入一个元素（数组前面）     |                                                              |


### 栈:

压栈:先进后出(FILO)

```php
//先压栈后出栈,都是从一段进出
$arr = array();
array_push($arr, 3);
array_push($arr, 2);
array_push($arr, 1);
print_r($arr);	//Array ( [0] => 3 [1] => 2 [2] => 1 )
echo  '<br/>';
echo array_pop($arr), '<br/>';	//1
echo array_pop($arr), '<br/>';	//2
echo array_pop($arr),'<br/>';	//3
```



### 队列:

排队,先进先出

```php
<?php
//先压栈后出栈,都是从一段进出
$arr = array();
array_unshift($arr, 3);
array_unshift($arr, 2);
array_unshift($arr, 1);
print_r($arr);	//Array ( [0] => 1 [1] => 2 [2] => 3 )
echo  '<br/>';
echo array_pop($arr), '<br/>';	//3
echo array_pop($arr), '<br/>';	//2
echo array_pop($arr),'<br/>';	//1
?>
```

## array_reverse() 数组元素反过来

```php
<?php
$arr = array(1,2,3,7,9);
print_r(array_reverse($arr)) ;//Array ( [0] => 9 [1] => 7 [2] => 3 [3] => 2 [4] => 1 )
?>
```

## in_array() 判断一个元素是否在数组中存在

返回值: bool(true/false)

```
<?php
$arr = array(1,2,3,7,9);
var_dump(in_array(6,$arr));
?>
```

## array_keys()：获取一个数组的所有下标，返回一个索引数组

## array_values()：获取一个数组的所有值，返回一个索引数组

# 编程思想

利用数学模式,来解决对应的需求问题, 然后利用代码实现对应的数据模型(逻辑)
算法:使用代码实现对应的数学模型,从而解决对应的业务问题

递归

### 斐波那契数列

```php
<?php
$f[1] = 1;
$f[2] = 1;
$des = 15;
for ($i=3; $i <$des; $i++){
    $f[$i] = $f[$i - 1] + $f[$i - 2];
}
print_r($f); //Array ( [1] => 1 [2] => 1 [3] => 2 [4] => 3 [5] => 5 [6] => 8 [7] => 13 [8] => 21 [9] => 34 [10] => 55 [11] => 89 [12] => 144 [13] => 233 [14] => 377 )
?>
```

```php
function my_recursive($des){
    $arr = array();
    $arr[1] = 1;
    $arr[2] = 1;

    $i = 3;
    while($i<=$des){
        $arr[$i] = $arr[$i - 1] + $arr[$i - 2];
        $i++;
    }
    return $arr[$des];
}
print_r(my_recursive(15));//610
```

## 递归

递归算法是把问题转为 规模缩小了的 同类问题的子问题 然后递归调用函数 来表示问题的解

> 1.简化问题: 找到最优子问题
>
> 2.函数自己调用自己

递归思想中：有两个非常重要的点

> 递归点：发现当前问题可以有解决当期问题的函数，去解决规模比当前小一点的问题来解决
>  F(N) = F(N - 1) + F(N - 2);
>
> 递归出口：当问题解决的时候，已经到达（必须有）最优子问题，不能再次调用函数
>
> 如果一个函数递归调用自己而没有递归出口：就是死循环

递归的本质是函数调用函数：一个函数需要开辟一块内存空间，递归会出现同时调用N多个函数（自己）：递归的本质是利用空间换时间

```php
//递归
function recursive($des){
    if(3<=$des){
        return recursive($des -1) + recursive($des - 2);
    }
    return 1;
}
print_r(recursive(15));
```

# 数组排序算法

## 冒泡排序（Bubble Sort）

一种计算机科学领域的较简单的排序算法。

它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。

> 冒泡排序的算法思路：
>
> 1） 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
>
> 2） 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。
>
> 3） 针对所有的元素重复以上的步骤，除了最后一个。
>
> 4） 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```php
<?php
//冒泡排序
$arr = array(1,9,11,3,5,2,7,8);
$new_arr = array();
for ($i = 0; $i < count($arr); $i++){
    for ($j = 0; $j < count($arr)-$i -1; $j++){
        if ($arr[$j] > $arr[$j+1]){
            $temp = $arr[$j];
            $arr[$j] = $arr[$j +1];
            $arr[$j + 1] = $temp;
        }
    }
}
print_r($arr);
?>
```

## 选择排序 Selection sort

选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，直到全部待排序的数据元素排完。 选择排序是不稳定的排序方法（比如序列[5， 5， 3]第一次就将第一个[5]与[3]交换，导致第一个5挪动到第二个5后面）。

选择排序的算法思路：
1）	假设第一个元素为最小元素，记下下标。
2）	寻找右侧剩余的元素，如果有更小的，重新记下最新的下标。
3）	如果有新的最小的，交换两个元素。
4）	往右重复以上步骤，直到元素本身是最后一个。

```php
<?php
//选择排序
$arr = array(1,9,11,3,5,2,7,8);
for ($i = 0; $i < count($arr); $i++){
    $min = $i;
    for ($j = $i + 1; $j < count($arr); $j++){
        if ($arr[$j] < $arr[$min]){
            $min = $j;
        }
    }
    if ($i != $min){
        $temp = $arr[$i];
        $arr[$i] = $arr[$min];
        $arr[$min] = $temp;
    }
}
print_r($arr);
?>
```

## 插入排序 Insert sort

插入排序（Insert sort）,插入排序的基本操作就是将一个数据插入到已经排好序的有序数据中，从而得到一个新的、个数加一的有序数据，算法适用于少量数据的排序，是稳定的排序方法。插入算法把要排序的数组分成两部分：第一部分包含了这个数组的所有元素，但将最后一个元素除外（让数组多一个空间才有插入的位置），而第二部分就只包含这一个元素（即待插入元素）。在第一部分排序完成后，再将这个最后元素插入到已排好序的第一部分中。
插入排序的基本思想是：每步将一个待排序的纪录，按其关键码值的大小插入前面已经排序的文件中适当位置上，直到全部插入完为止。

插入排序的算法思路：
1） 设置监视哨r[0]，将待插入纪录的值赋值给r[0]；
2） 设置开始查找的位置j；
3） 在数组中进行搜索，搜索中将第j个纪录后移，直至r[0].key≥r[j].key为止；
4） 将r[0]插入r[j+1]的位置上。

1、	认定第一个元素已经排好序；
2、	取出第二个元素，作为待插入数据；
3、	与已经排好序的数组的最右侧元素开始进行比较
4、	如果后面的小于前面的：说明前面已经排好序的那个数组元素不在对的位置（向后移一个），然后让新的元素填充进去（继续向前比：高级）
5、	重复前面的步骤：直到当前元素插入到对位置；
6、	重复以上步骤，直到所有的数组元素都插入到对的位置。

```php
<?php
//插入排序
$arr = array(1,9,11,3,5,2,7,8);
for ($i=1;$i<count($arr);$i++){
    $temp = $arr[$i];
    for ($j = $i-1; $j>=0; $j--){
        if ($arr[$j] > $temp){
            $arr[$j + 1] = $arr[$j];
            $arr[$j] = $temp;
        }else{
            break;
        };
    }
}
print_r($arr);

?>
```

## 快速排序  Quicksort

快速排序（Quicksort）是对冒泡排序的一种改进。通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。（递归）

设要排序的数组是A[0]……A[N-1]，首先任意选取一个数据（通常选用数组的第一个数）作为关键数据，然后将所有比它小的数都放到它前面，所有比它大的数都放到它后面，这个过程称为一趟快速排序。值得注意的是，快速排序不是一种稳定的排序算法，也就是说，多个相同的值的相对位置也许会在算法结束时产生变动。

快速排序的算法是：
1）	从数组中选出一个元素（通常第一个），作为参照对象。
2）	定义两个数组，将目标数组中剩余的元素与参照元素挨个比较：小的放到一个数组，大的放到另外一个数组。
3）	第二步执行完之后，前后的数组顺序不确定，但是确定了自己的位置。
4）	将得到的小数组按照第1到第3部重复操作（子问题）。
5）	回溯最小数组（一个元素）。

```php
<?php
//快排
$arr = array(1,9,11,3,5,2,7,8);
function quik_sort($arr){
    $len = count($arr);
    if ($len <= 1){return $arr;};
    $left = $right = array();
    for ($i = 1; $i < $len; $i++){
        if ($arr[$i] < $arr[0]){
            $left[] = $arr[$i];
        }else{
            $right[] = $arr[$i];
        }
    }
    $left = quik_sort($left);
    $right = quik_sort($right);
    return array_merge($left,(array)$arr[0], $right);
}
print_r(quik_sort($arr));
?>
```



# 归并排序 MERGE-SORT

归并排序（MERGE-SORT）是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。

二路归并实现：

```php
<?php
//二路并归
$arr1 = array(1, 7, 9);
$arr2 = array(2, 4, 6);
$arr = array();
while(count($arr1) && count($arr2)){
    $arr[] = $arr1[0] < $arr2[0] ? array_shift($arr1) : array_shift($arr2);
}
print_r(array_merge($arr, $arr2, $arr1));
?>
```

归并排序的算法是：

1） 将数组拆分成两个数组。

2） 重复步骤1将数组拆分成最小单元。

3） 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列.

4） 设定两个指针，最初位置分别为两个已经排序序列的起始位置。

5） 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置。

6） 重复步骤3直到某一指针超出序列尾。

7） 将另一序列剩下的所有元素直接复制到合并序列尾。

```php
<?php
//归并排序
$arr = array(1,9,11,3,5,2,7,8);
function merge_sort($arr){
    $len = count($arr);
    if ($len <= 1){return $arr;}
    $middle = floor($len/2);
    $left = array_slice($arr, 0, $middle);
    $right = array_slice($arr, $middle);
    $left = merge_sort($left);
    $right = merge_sort($right);
    $arr1 = array();
    while (count($left) && count($right)){
        $arr1[] = $left[0] < $right[0] ? array_shift($left) : array_shift($right);
    }
    return array_merge($arr1, $left, $right);
}
print_r(merge_sort($arr));
?>
```



## 查找算法

查找算法含义
查找是在大量的信息中寻找一个特定的信息元素，在计算机应用中，查找是常用的基本运算。查找算法是指实现查找过程对应的代码结。就是中大型数组中去快速定位想要的元素。

### 顺序查找算法

顺序查找也称为线形查找，从数据结构线形表的一端开始，顺序扫描，依次将扫描到的结点关键字与给定值k相比较，若相等则表示查找成功；若扫描结束仍没有找到关键字等于k的结点，表示查找失败。

```php
<?php
//归并排序
$arr = array(1,9,11,3,5,2,7,8);
function check_order($arr, $num){
    if (!count($arr)){return false;}
    for ($i = 0; $i < count($arr); $i++){
        if ($arr[$i] == $num){
            return $i;
        }
    }
    return false;
}
var_dump(check_order($arr,15));
?>
```



### 二分查找算法

二分查找要求线形表中的结点按关键字值升序或降序排列，用给定值k先与中间结点的关键字比较，中间结点把线形表分成两个子表，若相等则查找成功；若不相等，再根据k与该中间结点关键字的比较结果确定下一步查找哪个子表，这样递归进行，直到查找到或查找结束发现表中没有这样的结点。

折半算法思路：

1、  计算数组长度；

2、  确定左右两边的指针位置；

3、  找到中间位置；

4、  匹配

5、  然后根据大小重定边界



[TOC]