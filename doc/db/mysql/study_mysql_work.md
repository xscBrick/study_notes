# study_mysql_work

[TOC]



## 更新字段 update set

```php
$sql = "update t_vpcgw_query_switch_log set updateTime=?";
$data[]= date('Y-m-d H:i:s',time());

if(isset($param['flag'])){
    $sql .= " ,flag = ? ";
    $data[]= $param['flag'];
}

$sql .= "where id = ?";
$data[] = $param['id'];
$res = $db->query($sql, $data);
```

```mysql
update table_name set column1='new_value',column2='new_value2' where id = 35;
```

```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'UPDATE runoob_tbl
        SET runoob_title="学习 Python"
        WHERE runoob_id=3';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法更新数据: ' . mysqli_error($conn));
}
echo '数据更新成功！';
mysqli_close($conn);
?>
```

## 增加字段 alter table add column

```mysql
alter table t_vpcgw_query_switch_log 
add column `old_target_weight` int(10) NOT NULL after `weight`,
add column  `flag` int(1) DEFAULT 1 after `old_weight`,
modify column `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT;
```

## 增加索引 alter table add index

```mysql
ALTER TABLE `t_vpcgw_query_switch_log` ADD INDEX ( `region`, `vpcId`, `uniqVpcgwId` );
```

## 修改字段 alter table modify column

```mysql
alter table t_vpcgw_query_switch_log 
add column `old_target_weight` int(10) NOT NULL after `weight`,
add column  `flag` int(1) DEFAULT 1 after `old_weight`,
modify column `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT;
```



```mysql
alter table t_modify_vpcgw_weight_task
modify column vpcdata mediumtext default null;
```



## 创建表 create table

```mysql
CREATE TABLE `t_vpcgw_query_switch_log` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `region` varchar(10) NOT NULL,
  `name` varchar(100) DEFAULT NULL,
  `uniqVpcgwId` varchar(100) DEFAULT NULL,
  `weight` int(10) NOT NULL,
  `old_target_weight` int(10) NOT NULL,
  `vpcId` int(10) NOT NULL,
  `old_region` varchar(10) NOT NULL,
  `old_name` varchar(100) NOT NULL,
  `old_uniqVpcgwId` varchar(100) NOT NULL,
  `old_weight` int(10) NOT NULL,
  `flag` int(1) DEFAULT 1,
  `updateTime` datetime NOT NULL,
  PRIMARY KEY (`id`)
  INDEX (`vpcId`,`region`)
) ENGINE=MyISAM AUTO_INCREMENT=32 DEFAULT CHARSET=utf8
```

## 连接数据库

```shell
mysql -h10.249.50.199 -P10417 -uroot -p62Ds1%sTmP -Dapollo 
```

## Db_model.php

```mysql
ca(北美): mysql -h10.116.19.172 -P6136 -uslaveroot -pvpc_query -Ddb_tvpc -A
apollo: mysql -h10.249.50.199 -P10417 -uroot -p62Ds1%sTmP -Dapollo -A
db_tvpc,ca: mysql -h10.116.19.172 -P3470 -uvpc_query -pvpc_query -Ddb_tvpc -A
vstation , ca : mysql -h10.116.19.172 -P6136 -uslaveroot -p79zKbm_M4F -Ddb_vstation -A
   
```

## mysql 插入数据

```php
$db = $this->load->database($dbConfig, TRUE);
    if(is_array($values)){
        $valuesStr = json_encode($values);
        $sql = "INSERT INTO `t_config` (`property`, `value`) VALUES(?, ?) ON DUPLICATE KEY UPDATE `value`=?";
        $query = $db->query("set NAMES utf8");
        $result = $db->query($sql, array($property, $valuesStr, $valuesStr));
        return $result;
    }
    return false;
```

## concat('m','y','s','q','l') 连接几个字符串

## left(str,length)

## substring_index(str,delim,count)

```mysql
//concat 连接几个字符串，concat('m','y','s','q','l'),left(str,length)
select *, (select count(*)  from t_ipv6_vpc as vpc where t_ipv6_vpc.flag = 1 and t_ipv6_vpc.address like  as use_num from t_ipv6_section as section;

//截取字符串，substring_index(str,delim,count),字符串，分隔符，位置
select *,substring_index(t_ipv6_section.address, "::",1), (select count(*)  from t_ipv6_vpc where flag = 1 and address like concat("%", substring_index(t_ipv6_section.address, "::",1), "%"))  as use_num from t_ipv6_section;
```



## mysql 查询插入新字符

```mysql
select *, (select count(*) from table_b where flag=1) as new_columin from table_a;
```

