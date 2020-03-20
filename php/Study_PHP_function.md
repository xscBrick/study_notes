# Study_PHP_function

[TOC]



## rtrim() 删除函数末端空白字符或其他字符

```php
rtrim ( string $str [, string $character_mask ] ) : string
```

```php
//批量插入
public function insertMigrateVip($param){
    $data = array();
    $dbHandle = $this->getApolloDbHandle();
    $sql = "replace into `t_migrate_vip`(region,vpcid,vip) values ";
    foreach($param as $row){
        $sql .= "(?,?,?),";
        $data[] = $row['region'];
        $data[] = $row['vpcId'];
        $data[] = $row['vip'];
    }
    //删除末端 逗号
    $sql = rtrim($sql, ',');
    $dbHandle->query($sql, $data);
    return $dbHandle->insert_id();
}
```

### ::class[ ](https://www.php.net/manual/zh/language.oop5.basic.php#language.oop5.basic.class.class)

关键词 *class* 也可用于类名的解析。使用 *ClassName::class* 你可以获取一个字符串，包含了类 *ClassName* 的完全限定名称。这对使用了 [命名空间](https://www.php.net/manual/zh/language.namespaces.php) 的类尤其有用。

### extends[ ](https://www.php.net/manual/zh/language.oop5.basic.php#language.oop5.basic.extends)

一个类可以在声明中用 *extends* 关键字继承另一个类的方法和属性。PHP不支持多重继承，一个类只能继承一个基类。

被继承的方法和属性可以通过用同样的名字重新声明被覆盖。但是如果父类定义方法时使用了 [final](https://www.php.net/manual/zh/language.oop5.final.php)，则该方法不可被覆盖。可以通过 [parent::](https://www.php.net/manual/zh/language.oop5.paamayim-nekudotayim.php) 来访问被覆盖的方法或属性。

当覆盖方法时，参数必须保持一致否则 PHP 将发出 **E_STRICT** 级别的错误信息。但构造函数例外，构造函数可在被覆盖时使用不同的参数。

### new[ ](https://www.php.net/manual/zh/language.oop5.basic.php#language.oop5.basic.new)

要创建一个类的实例，必须使用 *new* 关键字。当创建新对象时该对象总是被赋值，除非该对象定义了[构造函数](https://www.php.net/manual/zh/language.oop5.decon.php)并且在出错时抛出了一个[异常](https://www.php.net/manual/zh/language.exceptions.php)。类应在被实例化之前定义（某些情况下则必须这样）。

如果在 *new* 之后跟着的是一个包含有类名的字符串 [string](https://www.php.net/manual/zh/language.types.string.php)，则该类的一个实例被创建。如果该类属于一个命名空间，则必须使用其完整名称。

在类定义内部，可以用 *new self* 和 *new parent* 创建新对象。

当把一个对象已经创建的实例赋给一个新变量时，新变量会访问同一个实例，就和用该对象赋值一样。此行为和给函数传递入实例时一样。可以用[克隆](https://www.php.net/manual/zh/language.oop5.cloning.php)给一个已创建的对象建立一个新实例。

### class[ ](https://www.php.net/manual/zh/language.oop5.basic.php#language.oop5.basic.class)

每个类的定义都以关键字 *class* 开头，后面跟着类名，后面跟着一对花括号，里面包含有类的属性与方法的定义。

类名可以是任何非 PHP [保留字](https://www.php.net/manual/zh/reserved.php)的合法标签。一个合法类名以字母或下划线开头，后面跟着若干字母，数字或下划线。以正则表达式表示为：*[a-zA-Z_\x7f-\xff][a-zA-Z0-9_\x7f-\xff]**。

一个类可以包含有属于自己的[常量](https://www.php.net/manual/zh/language.oop5.constants.php)，[变量](https://www.php.net/manual/zh/language.oop5.properties.php)（称为“属性”）以及函数（称为“方法”）。

当一个方法在类定义内部被调用时，有一个可用的伪变量 $this。$this 是一个到主叫对象的引用（通常是该方法所从属的对象，但如果是从第二个对象[静态](https://www.php.net/manual/zh/language.oop5.static.php)调用时也可能是另一个对象）。

```

```

## date() 时间函数

```php
$time = date('Y-m-d H:i:s',time());
```

