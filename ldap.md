# LDAP

LDAP的全称是"轻量级目录访问协议(Lightweight Directory Access Protocol)"，它是一种简单的目录协议，所谓目录，是一种专门的数据库，可以用来服务于任何应用程序。

LDAP协议是一种跨平台的标准协议，当应用程序通过LDAP协议问题LDAP目录时，不需要考虑LDAP所在的服务器类型和操作系统类型，可以直接对LDAP目录中的内容进行读写。

## OpenLDAP配置

OpenLDAP安装目录下的slapd.conf文件是OpenLDAP服务器的配置文件。在启动OpenLDAP服务之前，需要首先修改该文件对OpenLDAP进行配置。主要改动包括以下:

- 包含更多的schema文件。 schema文件是OpenLDAP提供的存储模式，在这里包含相应的模式文件可以使OpenLDAP使用应用的模式进行数据存储和管理。
- 配置服务器根目录信息。修改slapd.conf文件中的suffix可以修改服务器的根目录信息，所有的其他数据都将建立在这个根目录上。`suffix "dc=simon,dc=com"`
- 设置管理员用户名和密码。修改rootdn中的cn值可以修改管理员账户，修改rootpw的值可以修改账户的密码

```
rootdn "cn=admin,dc=simon,dc=com"
rootpw pass
```

### OpenLDAP启动与关闭

- 启动OpenLDAP的命令如下:

```bash
slapd start
```

- 关闭OpenLDAP的命令如下:

```bash
slapd stop
```

### OpenLDAP数据操作

使用OpenLDAP安装目录下的ldapadd命令可以实现向LDAP目录中增加数据，具体命令如下:

```bash
ldapadd -x -D "cn=admin,dc=simon,dc=com" -W
```

其中，-x表示使用简单验证方式，-D及其后面的参数表示当前的根目录和账户信息，-W表示当前管理员登录需要使用密码进行身份验证。命令运行后，提示需要输入密码，输入密码后，就可以向LDAP目录中输入数据了，输入数据如下:

```
dn:dc=simon,dc=com
objectClass:dcObject
objectClass:organization
dc:simon
o:company
description:this is a test
```

其中,dn表示根目录信息。objectClass表示对象的类别，即在OpenLDAp模式中指定的属性。后而的dc、o和description分别表示数据的属性。数据输入后，按Ctrl+Z完成输入。
在添加数据后，可使用ldapsearch命令查看数据，命令如下:

```bash
ldapsearch -X -b "dc=simon,dc=com"
```

其中，-X表示使用简单验证方式，-c及其后面的参数表示要进行查询的根目录信息。

## PHP配置LDAP

激活LDAP的扩展方法是找到PHP安装目录下的php.ini文件，在其中找到如下代码:

```INI
;extension=php_ldap.dll
```

去掉前面的分号，然后重新启动Apache服务器就可以完成配置了。

## PHP操作LDAP

### 连接LDAP服务器

PHP中用于连接LDAP服务器的函数是ldap_connect，其语法格式如下:

```PHP
ldap_connect([string hostname [, int port]])
```

其中`hostname`是LDAP服务器所在的主机地址,`port`是LDAP服务器的端口号。

### 绑定LDAP服务器

绑定LDAP服务器的含义是使用特定的用户名和密码来登录LDAP服务器。PHP中用户绑定LDAP服务器的函数是`ldap_bind`，其语法格式如下:

```PHP
ldap_bind(ldap_conn [, string username [, string password]])
```

其中,`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`username`是登录LDAP服务器时使用的用户名，`password`是登录时所用的密码。

### 断开LDAP服务器

LDAP服务器断开的过程与绑定LDAP服务器相反，PHP中用于断开LDAP服务器的函数是`ldap_unbind`，其语法格式如下:

```PHP
ldap_unbind(ldap_conn)
```

其中，`ldap_conn`是前面连接LDAP服务器时创建的连接对象。

### 查询LDAP目录内容

查询LDAP目录使用`ldap_search`函数来实现，其语法格式如下:

```PHP
ldap_search(ldap_conn,bash_dn,conditions)
```

其中,`ldap_conn`是前面连接LDAP服务器时创建的连接对象。`base_dn`是LDAP服务器的查询主键。`conditions`是LDAP目录查询所用的条件。该函数返回一个结果对象。该结果对象保存查询到的所有记录。

对于这个结果对象，可以使用`ldap_get_entries`函数进行读取，其语法格式如下:

```PHP
ldap_get_entries(ldap_conn,result)
```

其中，`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`result`是前面查询LDAP目录时返回的对象。该函数返回一个数组，包含所有的结果记录。

### 获得查询结果中的值

PHP还提供了专门用于获得查询结果值的方法。

首先介绍一种与`ldap_get_entries`相似的函数`ldap_first_entry`，该函数仅获得结果对象中的第一条记录，其语法格式如下：

```PHP
ldap_first_entry(ldap_conn,result)
```

其中`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`result`是前面查询LDAP目录时返回的对象。

获取结果中的值的函数为`ldap_get_values`，该函数的语法格式如下:

```PHP
ldap_get_values(ldap_conn,entry,column)
```

其中`ldap_conn`是前面连接LDAP服务器创建的连接对象, `entry`是前面获得查询结果时返回的对象，`column`是要返回的值所在的列的名称。该函数返回一个仅包含该列信息的数组。

### 计算查询结果中的记录数

计算查询结果中的记录数用`ldap_count_entries`函数来实现，该函数的语法格式如下:

```PHP
ldap_count_entries(ldap_conn,result)
```

其中，`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`result`是前面查询LDAP目录时返回的对象，

### 添加一条新记录

向LDAP添加一条新记录使用`ldap_add`函数来完成

```PHP
ldap_add(ldap_conn,base_dn,entry)
```

其中，`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`base_dn`是LDAP服务器的查询主键，`entry`是储存新记录的数组。

### 更新记录

更新LDAP中的一条记录使用`ldap_modify`函数来完成

```PHP
ldap_modify(ldap_conn,base_dn,entry)
```

其中`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`base_dn`是LDAP服务器的查询主键，`entry`是储存更新后的记录的数组。

### 删除记录

删除LDAP中的一条记录使用`ldap_delete`函数来完成

```PHP
ldap_delete(ldap_conn,base_dn)
```

其中`ldap_conn`是前面连接LDAP服务器时创建的连接对象，`base_dn`是LDAP服务器的查询主键。

### 错误处理

PHP还提供了对LDAP操作的错误进行处理的方法

`ldap_errno`的语法格式如下:

```PHP
int ldap_errno(resource)
```

其中`resource`是LDAP操作中产生的对象，该函数返回一个错误代码。

`ldap_error`的语法格式如下:

```PHP
string ldap_error(resource)
```

其中`resource`是LDAP操作中产生的对象，该函数返回一个错误信息。

`ldap_err2str`语法格式如下:

```PHP
string ldap_err2str(int errno)
```

其中`errno`是前面返回的错误代码，该函数将返回一个错误信息。
