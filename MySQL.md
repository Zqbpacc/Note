## 数据库

数据库（Database）是按照数据结构来组织、存储和管理数据的仓库。

特点：

- 1.数据以表格的形式出现
- 2.每行为各种记录名称
- 3.每列为记录名称所对应的数据域
- 4.许多的行和列组成一张表单
- 5.若干的表单组成database



## `MySQL`

​		`MySQL `是一个**`关系型数据库管理系统`**（瑞典Oracle 公司），`MySQL` 是一种关联数据库管理系统，关联数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，增加了速度并提高了灵活性。

**`MySQL`的特点**：

- MySQL 是开源的，所以你不需要支付额外的费用。
- MySQL 支持大型的数据库。可以处理拥有上千万条记录的大型数据库。
- MySQL 使用标准的 SQL 数据语言形式。
- MySQL 可以运行于多个系统上，并且支持多种语言。这些编程语言包括 C、C++、Python、Java、Perl、PHP、Eiffel、Ruby 和 Tcl 等。
- MySQL 对PHP有很好的支持，PHP 是目前最流行的 Web 开发语言。
- MySQL 支持大型数据库，支持 5000 万条记录的数据仓库，32 位系统表文件最大可支持 4GB，64 位系统支持最大的表文件为8TB。
- `MySQL `是可以定制的，采用了` GPL `协议，你可以修改源码来开发自己的 `MySQL `系统。

​		

​		`MySQL `为关系型数据库(Relational Database Management System), 这种所谓的"关系型"可以理解为 **`"表格"`** 的概念, **一个关系型数据库由一个或数个表格组成**。

**组成**： 

- 表头(header): 每一列的名称;
- 列(col): 具有相同数据类型的数据的集合;
- 行(row): 每一行用来描述某条记录的具体信息;
- 值(value): 行的具体信息, 每个值必须与该列的数据类型相同;
- **键(key)**: 键的值在当前列中具有唯一性。





### `MySQL`语句

![](E:\Note\前后端交互流程图.png)

```
-- select * from user
-- select password from user
-- select * from user where id=1
-- select username from user where id=1
-- select * from user where id=1 and username="zhangsan"
-- select * from user order by id desc
-- select * from user limit 1
-- select * from user limit 1,2
-- select * from user where username like '%a%'


-- insert into user (username,password) values ("zhaosi", "789")
-- delete from user where id=5
-- update user set password=666 where id=4
```





#### PHP配置MySQL

* 配置

  ```php
  <?php
    $config = array(
      "host" => "localhost:3306",
      "dbname" => "1902",
      "username" => "root",
      "password" => ""
  
    );
    // 跟数据库建立连接
    mysql_connect($config['host'], $config['username'], $config['password']);
    // 选择数据库
    mysql_select_db($config['dbname']);
  
    // 设置编码
    mysql_query("set charset 'utf8'");
    mysql_query("set character set 'utf8'");
  
  ?>
  ```

* 插入

  ```php
  <?php
    // 引入另外一个php文件
    include("./config.php");
  
    // 新增
    // 书写sql语句
    $username = "喜羊羊";
    $password = "111";
    // 再php里，双引号可以直接解析变量(单引号不行)
    $sql = "insert into user (username,password) values ('$username','$password')";
    
    // 执行sql语句
    $res = mysql_query($sql);
    // $res 是个boolean
    echo $res;
  ?>
  ```

* 查询

  ```php
  <?php
    // 引入另外一个php文件
    include("./config.php");
  
    // 查询
    // 书写sql语句
    $sql = "select * from user";
    // 执行sql语句
    $res = mysql_query($sql);
    // $res时资源类型
    $arr = array();
    while($row = mysql_fetch_assoc($res)){
      array_push($arr, $row);
    }
  
    echo json_encode($arr);
  ?>
  ```

* 更新

  ```php
  <?php
    // 引入另外一个php文件
    include("./config.php");
  
    // 新增
    // 书写sql语句
    $username = "美羊羊";
    $password = "333";
    $id=7;
    // 再php里，双引号可以直接解析变量(单引号不行)
    $sql = "update user set username='$username',password='$password' where id=$id";
    
    // 执行sql语句
    $res = mysql_query($sql);
    // $res 是个boolean
    echo $res;
  ?>
  ```

  



