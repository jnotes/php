# 网络客户端

`fsockopen`是一个通过Socket套接字协议来访问远程主机的函数，PHP访问远程主机可以使用该函数来实现。在使用`fsockopen`打开远程web服务器以后，可以通过直接向页面内写入数据来实现表单的提交。其语法格式如下:

```PHP
fsockopen(string host,int port [,int errno [,string errstr [, float timeout]]])
```

其中,`host`表示远程主机的地址，`port`表示用于连接的端品号，`errno`和`errstr`分别表示连接过程中可能遇到的错误代码和错误消息，如果没有错误，则`errno`为0, `timeout`是用户设置的最大尝试连接时间。

## PHP访问FTP服务器

连接FTP服务器是使用`ftp_connect`函数来实现的，其语法格式如下:

```PHP
ftp_connect(string $host,[int $port [, int $timeout])
```

其中`$host`表示FTP主机的地址，`$port`表示端口号，`$timeout`表示超时时间。如果连接成功，该函数返回一个连接资源对象，否则返回`false`。

断开连接是使用`ftp_quit`函数来实现的，其语法格式如下:

```PHP
ftp_quit($conn)
```
其中`$conn`是使用`ftp_connect`函数连接服务器时返回的资源对象。

使用`ftp_systype($conn)`函数可以查看服务器的操作系统。

登录FTP服务器是使用`ftp_login`函数来实现

```PHP
ftp_login($conn,$username,$password)
```

PHP提供两种获取FTP文件列表的方式，最常用的是使用`ftp_nlist`函数，该函数可以读取指定目录下的全部文件，并将文件名保存到数组中，语法格式如下:

```PHP
ftp_nlist($conn,string $directory)
```

其中，`$conn`是使用`ftp_connect`函数连接服务器时返回的资源对象，`$directory`是要读取的目录。

另外一种获取FTP文件列表的方式是使用`ftp_rawlist`函数，该函数返回指定目录下的全部目录和文件，并在数组中保存详细信息。基语法格式与`ftp_nlist`相同。

`ftp_put`函数来实现文件的上传，其语法格式如下:

```PHP
ftp_put($conn,string $remote_file,string $local_file,int $mode)
```

其中，`$conn`是使用`ftp_connect`函数连接服务器时返回的资源对象。`$remote_file`是上传后的远程文件名，`$local_file`是本地文件名。`$mode`是传输模式，可以是`FTP_ASCII`(文本模式)或`FTP_BINARY`(二进制模式)。如果上传成功返回`true`。否则为`false`

`ftp_get`函数来实现文件的下载，其语法格式如下:

```PHP
ftp_get($conn,string $local_file,string $remote_file,int $mode)
```

其中，`$conn`是使用`ftp_connect`函数连接服务器时返回的资源对象。`$local_file`是下载后的本地文件名,`$remote_file`是远程文件名。`$mode`是传输模式，可以是`FTP_ASCII`(文本模式)或`FTP_BINARY`(二进制模式)。如果下载成功返回`true`。否则为`false`

`ftp_delete`函数来实现删除文件，其语法格式如下:

```PHP
ftp_delete($conn,string $remote_file)
```

其中，`$conn`是使用`ftp_connect`函数连接服务器时返回的资源对象。`$remote_file`是要被删除的文件名。如果删除成功，返回为`true`,否则为`false`

`ftp_mkdir`函数用来实现创建目录，其语法格式如下

```PHP
ftp_mkdir($conn,$dir)
```

`ftp_rmdir`函数用来实现删除目录，其语法格式如下

```PHP
ftp_rmdir($conn,$dir)
```
