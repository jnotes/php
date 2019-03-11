# 数据库

## PHP操作数据库

PHP操作数据库是通过MYSQL扩展来实现的，`php.ini`文件中的`extension`参数用于配置PHP的扩展库。用法如下:

```
extension=<filename>
```

其中，filename指代扩展库的文件名，MYSQL的扩展加文件名为`php_mysql.dll`，因此，可以通过查看`php.ini`文件中是否包含以下语句来检查当前的PHP环境中的MYSQL是否可用。

如果这个语句不存在，则需要在`php.ini`文件的未尾添加这条语句。添加后重新启动Apache服务器即可。

### 数据库的连接与断开

#### 连接

连接数据库服务器通过`mysql_connect`函数来实现，语法格式工如下:

```PHP
mysql_connect(string hostname [, string username [, string password]]);
```

这里的`hostname`是数据库服务器所在的主机地址或IP,`username`是库连用户名,`password`是连接密码。该函数返回一个资源类型的变量用来提供与数据库的库接。

#### 断开

与数据库服务器断开通过`mysql_close`函数来完成

### 选择数据库

选择数据库通过`mysql_select_db`函数来实现，语法格式如下:

```PHP
bool mysql_select_db(string database_name [, resource_id])
```

这里的`database_name`是要选择的数据库名,`resource_id`是前面连接数据库是返回的对象。

### 执行SQL语句

通过`mysql_query`函数来执行SQL语句，语法格式如下:

```PHP
mysql_query(string sql_statement [,resource_id])
```

这里的`sql_statement`是要执行的SQL语句，`resource_id`是前面连接数据库是返回的对象。该函数返回一个资源型变量，用来存储SQL的执行结果。

除了`mysql_query`以外，PHP还提供了一个类似的函数`mysql_db_query`，该函数完成与`mysql_query`完成相同的功能。区别在于`mysql_db_query`函数支持在执行SQL语句的同时选择数据库。语法格式如下:

```PHP
mysql_db_query(string database_name, string sql_statement [,resource_id])
```

这里的`database_name`是要选择的数据库名，`sql_statement`是要执行的SQL语句，`resource_id`是前面连接数据时返回的对象，与`mysql_query`中的参数用法相同。

### 获得查询记录数

`mysql_numrows`函数用于获得结果集中的记录数，语法格式如下:

```PHP
int mysql_numrows(result_set)
```

其中,`result_set`是前而返回的结果集变量名。该函数返回一个整型变量表示结果集中一共有多少条数据。

### 获得结果集中的某条记录

`mysql_result`函数用于获得结果集中的记录数,语法格式如下：

```PHP
mysql_result(result_set, int row [,field])
```

其中`result_set`是前面返回的结果集变量名，`row`是要返回记录所在行的行号,`field`是要返回的列名。

### 读取结果集

`mysql_fetch_row`函数用于读取结果集中的记录，语法格式如下：

```PHP
mysql_fetch_row(result_set)
```

其中,`result_set`是前面返回的结果集变量名。返回一个包含所有列的数组，数组的键按照列的顺序分配。

```PHP
mysql_fetch_array(result_set [,int type])
```

其中`result_set`是前面返回的结果集变量，`type`可以使用下面值中的一种：

- MYSQL_ASSOC：返回的数组的刍为数据库表中的列名
- MYSQL_NUM：返回的数组的键为数字。如果使用这个选项，则功能与`mysql_fetch_row`函数相同
- MYSQL_BOTH：返回的数组的键为数据库中的列名和数字。默认为这个选项。

## 获取数据库信息

`mysql_list_dbs`函数用于获取数据库列表，其语法如下:

```PHP
mysql_list_dbs([resource_id])
```
这里的`resource_id`是前面连接数据时返回的对象，该函数返回一个包含服务器上所有数据库名称的结果集。该结果集与使用`mysql_query`函数得到的结果集相同。

### 获取表信息

`mysql_list_tables`函数用于获取表的信息,其语法如下:

```PHP
mysql_list_tables(string database_name [, resource_id])
```

这里的`database_name`是数据库名，`resource_id`是前面连接数据库时返回的对象。该函数返回了一个包含有服务器上所有数据库名称的结果集，该结果集与`mysql_query`函数得到的结果集相同。

### 获取列的数目

`mysql_num_fields`函数用于获取列的数目，其语法如下:

```PHP
int mysql_num_fields(result_set)
```

其中`result_set`是`mysql_query`函数返回的结果集对象。

### 获取列名称

`mysql_field_name`函数用于获取列的名称，其语法如下:

```PHP
string mysql_field_name(result_set, int offset)
```

其中`result_set`是`mysql_query`函数返回的结果集对象，`offset`用来表示要返回的是第几列的名称。

### 获取列的数据类型

`mysql_field_type` 函数用于获取列的数据类型，其语法格式如下：

```PHP
string mysql_field_type(result_set,int offset)
```

其中`result_set`是`mysql_query`函数返回的结果集对象，`offset`用来表示要返回的是第几列的数据类型。

### 获取列的长度

`mysql_field_len`函数用来获取列的长度，其语法格式如下:

```PHP
int mysql_field_len(result_set,int offset)
```

其中`result_set`是`mysql_query`函数返回的结果集对象，`offset`用来表示要返回的是第几列的数据长度。

### 获取列的标志

`mysql_field_flag`函数用于获取列的标志。所谓标志，包括列的基本属性，其语法格式如下：

```PHP
int mysql_field_flag(result_set,int offset)
```

其中`result_set`是`mysql_query`函数返回的结果集对象，`offset`用来表示要返回的是第几列的标志。
