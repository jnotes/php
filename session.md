# Session与Cookie

Web应用是通过HTTP协议进行传输的，而根据HTTP协议的特点，客户端每次与服务器的对话都被当作一个单独的过程。用户从浏览器上访问第二个页面的时候，第一个页面的信息将不再被保存。

HTTP协议的这个特性为一些需要权限设置的安全页面编写造成了很大麻烦。

Session与Cookie技术也正是为了解决这个问题才诞生的。Session与Cookie的工作原理很类似。在用户访问初始页面时，服务器会为客户端分配一个SessionID或Cookit文件。然后在访问中，客户端每次访问服务器时发送SessionID或Cookie文件来表明自己的身份，服务器在接受到SessionID或Cookie文件时，会根据获得到的信息进行一些相关的动作，由此实现了信息在页面间传递的目的。

## Session

PHP在操作Session时，是将Session中的数据存储在服务器上，然后通过客户端传来的Session ID识别客户端信息，并进行相应的信息提取。PHP中的Session使用简单，并具可以定制服务器上的Session的存储方式，为Web应用的编写提供了方便。

### 开始使用 Session

`session_start`函数用户标识Session使用的开始，用于初始化Session变量，语法格式如下:

```PHP
session_start();
```

这个函数的返回值永远为布尔型的`TRUE`

### Session 预定义数组

在PHP中，Session的使用通常是通过一个预定义数组`$_SESSION`的调用和读取来完成的。在实际应用中，一个页面中对`$_SESSION`数组进行赋值，而在另一个页面中对`$_SESSION`数组进行读取，就可以实现变量在页面间的传递。如:

```PHP
// 赋值
$_SESSION['user'] = $user;

// 读取
echo $_SESSION['user'];
```

### Session 检测与注销

Session的检测与注销与对变量的操作完全相同，使用`isset`和`unset`函数来完成。可以在系统中通过检测Session是否已经被创建来检查用户的权限等。使用`isset`函数用于检测Session是否已经存在，语法格式如下：

```PHP
bool isset($_SESSION['user'])
```

如果名为`user`的Session已经建立，则返回`TRUE`。否则返回`FALSE`。

`unset`函数用于注销已经建立的SESSION变量，语法格式如下:

```PHP
unset($_SESSION['user'])
```

### Session 处理定制

在PHP中，Session的信息是存储在服务器上的，而且客户端与服务器间的对话仅通过SessionID来完成。PHP提供了三种存储Session的方式:文件存储、内存存储及自定义方式。

这三种存储方式的设置是通过修改PHP安装目录下的`php.ini`来完成的。

在定制Session的存储方式之前，首先要修改`php.ini`文件将存储方式设置为用户自定义方式。打开`php.ini`文件，设置

```
[session]
session.save_handler = files
```

将`session.save_handler`的值修改为`User`，然后重启服务器使修改生效。

使用用户自定义方式进行Session存储的具体实现是通过`session_set_save_handler`函数实现的，其语法格式如下:

```PHP
bool session_set_save_handler(string open,string close,string read,string write,string destroy,string gc)
```

函数中的六个参数用于实现Session存储的6个自定义函数名，这些函数的名称可以随意确定，但是其语法格式不能改变。

#### open

主要用于Session初始化，其语法格式如下:

```PHP
open(string save_path,string name)
```

其中，`save_path`是存放Session文件的路径，name是传递SessionID的Cookie名称。

#### close

主要用户处理页面结束时的相关操作，其语法格式如下:

```PHP
close()
```

该函数主要用于在页面结束时进行一些变量的清理工作。

#### read

要主用于读取Session，其语法格式如下:

```PHP
read(key)
```

用于读取Session时使用的键值

#### write

主要用于写入Session，其语法格式如下:

```PHP
write(key,data)
```

`key`是用于写入Session时使用的键值，`data`是存入Session的数据。

#### destroy

主要用于注销Session，其语法格式如下:

```PHP
destroy(key)
```

`key`主要用于注销Session的键值。

#### gc

主要用于清理过期的Session数据，其语法格式如下:

```PHP
gc(expiry_time)
```

其中`expiry_time`是Session保存时间的秒数

## Cookie

### 创建Cookie

创建一个Cookie是使用`setcookie`函及其前两个参数来实现的，只有使用前两个参数创建的Cookie与Session类似，在关闭浏览器后会自动注销。

PHP中的Cookie操作基本都是通过setcookie函数来实现的，语法格式如下:

```PHP
bool setcookie(string name [, string value [, int expire [, string path [, string domain [, int secure]]]]])
```

其中参数的意义如下:

- name: 表示Cookie的名字
- value: 表示Cookie的值
- expire: 表示Cookie的失效时间，是用秒数来表示的。
- path: 表示Cookie在服务器上的有效路径
- domain: 表示Cookie在服务器上的有效域名
- secure: 表示Cookie是否仅允许通过安全的HTTPS协议传输，1表示允许通过安全的HTTPS协议传输，0表示允许通过普通HTTP协议传输。

### 预定义数组

Cookie也提供了一个预定义数组`$_COOKIE`用于存储Cookie变量。

### 删除Cookie

删除Cookie是通过一个空值Cookie来实现的，即只指定`setcookie`函数的第一个参数，如:

```PHP
setcookie("user")
```

## 浏览器重定向

页面间的跳转通常使用header函数来实现的。使用header函数进行页面跳转的语法格式如下:

```PHP
header("location:url")
```

其中`url`表示要重定向的页面。
