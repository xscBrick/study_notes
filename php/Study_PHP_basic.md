# Study_PHP_basic

[TOC]



## ->,=>和::的区别



> php新手经常碰到的问题，->、=> 和 :: 这三个家伙是什么分别都是做什么的啊!看着就很晕。
> 没关系，下面我们做一下详细的解释，如果你有C++，Perl基础，你会发现这些家伙和他们里面的一些符号功能是差不多的。

->前面的变量是一个对象：

php‘- >’符号是“插入式解引用操作符”（infix dereference operator）。
换句话说，它是调用由引用传递参数的子程序的方法（当然，还有其它的作用）。正如我们上面所提到的，在调用PHP的函数的时候，大部分参数都是通过引用传递的。PHP中的‘->’功能就和它们在Perl或C++中一样。下面是一个简单的解引用的例子：

```php
$user->friends_count; //取对象的friends_count属性。
$t->homeTimeline($p); //调用对象的homeTimeline方法，方法中传入一个参数$p
```



在PHP的脚本中‘=>’操作符时很常见的。
因为php数组函数很丰富，我们要经常用到数组，因为它操作数据很方便。

```php
$phparr= new array( 
    in => 'reply,'
    side => 'left',
    padx => 2m,
    pady => 2m,
    ipadx => 2m,
    ipady => 1m
)
```

​    顺便说一下，如果你需要用数字“大于等于”的符号，你应该用“>=”而不是“=>”。
在PHP中“::”这个叫范围解析操作符，又名域运算符。
“::”符号可以认为是与C语言中的“.”相似的，而它更像C++中(Perl)的::类范围操作符。
php调用类的内部静态成员，或者是类之间调用就要用：：
下面是一个例子：

```php
class A
{
    static $count = 0;
    static function haha()
{
    //
}  
function diaoyoug()
{
    self::haha();
    self::$count;
}
}
a.b.c; /* C语言中的 */
a::b::c(); // C++ 中的函数
$a::b::c; # Perl 5中的标量
```

　　

## this,self,parent三个关键字从字面上比较好理解,分别是指这、自己、父亲。

this是指向当前对象的指针(姑且用C里面的指针来看吧)
==>this是指向当前对象实例的指针，不指向任何其他对象或类。

self是指向当前类的指针
==>self是指向类本身，也就是self是不指向任何已经实例化的对象，一般self使用来指向类中的静态变量。

parent是指向父类的指针(我 们这里频繁使用指针来描述，是因为没有更好的语言来表达)

根据实际的例子来看看

```php
//(1) this

1 <?php
2
3 class UserName
4 { 
5     //定义成员属性 
6     private $name;
7 
8     //定义构造函数
9     function __construct( $name )
10     {
11          $this->name = $name; //这里已经使用了this指针
12     }
13 
14     //析构函数
15     function __destruct(){}
16
17     //打印用户名成员函数
18     function printName()
19     {
20          print( $this->name ); //又使用了this指针
21     }
22 }
23
24 //实例化对象
25 $nameObject = new UserName( "heiyeluren" );
26
27 //执行打印
28 $nameObject->printName(); //输出: heiyeluren
29
30 //第二次实例化对象
31 $nameObject2 = new UserName( "PHP5" );
32
33 //执行打印
34 $nameObject2->printName(); //输出：PHP5
35 ?>
```


​    我们看，上面的类分别在11行和20行使用了this指针，那么当时this是指向谁呢？
​    其实this是在实例化的时候来确定指向谁，比如第一次实例化对象 的时候(25行)，那么当时this就是指向$nameObject对象，那么执行18行的打印的时候就把print( $this->name )变成了print( $nameObject->name )，那么当然就输出了"heiyeluren"。
​    第二个实例的时候，print( $this- >name )变成了print( $nameObject2->name )，于是就输出了"PHP5"。
所以说，this就是指向当前对象实例的指针，不指向任何其他对象或类。

(2)self

首先我们要明确一点，self是指向类本身，也就是self是不指向任何已经实例化的对象，一般self使用来指向类中的静态变量。

```php
1 <?php
2
3     class Counter
4     {
5         //定义属性，包括一个静态变量
6         private static $firstCount = 0;
7         private $lastCount;
8
9         //构造函数
10         function __construct()
11         {
12              $this->lastCount = ++selft::$firstCount; //使用self来调用静态变量,使用self调用必须使用::(域运算符号)
13         }
14
15         //打印最次数值
16         function printLastCount()
17         {
18              print( $this->lastCount );
19         } 
20     }
21
22 //实例化对象
23 $countObject = new Counter();
24
25 $countObject->printLastCount(); //输出 1
26
27 ?>
```

我 们这里只要注意两个地方，第6行和第12行。
我们在第二行定义了一个静态变量$firstCount，并且初始值为0，那么在12行的时候调用了这个值， 使用的是self来调用，并且中间使用"::"来连接，
就是我们所谓的域运算符，那么这时候我们调用的就是类自己定义的静态变量$frestCount， 我们的静态变量与下面对象的实例无关，它只是跟类有关，
那么我调用类本身的的，那么我们就无法使用this来引用，可以使用 self来引用，
因为self是指向类本身，与任何对象实例无关。换句话说，假如我们的类里面静态的成员，我们也必须使用self来调用。

(3)parent

我们知道parent是指向父类的指针，一般我们使用parent来调用父类的构造函数。

```php
1 <?php
2
3 //基类
4 class Animal
5 {
6     //基类的属性
7     public $name; //名字
8
9     //基类的构造函数
10     public function __construct( $name )
11     {
12          $this->name = $name;
13     }
14 }
15
16 //派生类
17 class Person extends Animal //Person类继承了Animal类
18 {
19     public $personSex; //性别
20     public $personAge; //年龄
21
22     //继承类的构造函数
23     function __construct( $personSex, $personAge )
24     {
25          parent::__construct( "heiyeluren" ); //使用parent调用了父类的构造函数
26          $this->personSex = $personSex;
27          $this->personAge = $personAge;
28     }
29
30     function printPerson()
31     {
32          print( $this->name. " is " .$this->personSex. ",this year " .$this->personAge );
33      }
34 }
35
36 //实例化Person对象
37 $personObject = new Person( "male", "21");
38
39 //执行打印
40 $personObject->printPerson(); //输出：heiyeluren is male,this year 21
41
42 ?>
```

我们注意这么几个细节：成员属性都是public的，特别是父类的，是为了供继承类通过this来访问。
我们注意关键的地方，第25行： parent::__construct( "heiyeluren" ),这时候我们就使用parent来调用父类的构造函数进行对父类的初始化，
因为父类的成员都是public的，于是我们就能够在继承类中直接使用 this来调用。

总结：this是指向对象实例的一个指针，self是对类本身的一个引用，parent是对父类的引用。