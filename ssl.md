# SSL

 在网络中，目前流行一种数据安全传输方式是使用SSL协议进行数据传输。SSL是安全套接层协议Secure Sockets Layer的缩写是网景公司推出的一个基于Web应用的安全协议。SSL协议通过一种架松在应用程序协议如HTTP、FTP等之上的安全层与数据传输的TCP/IP协议进行了数据安全分层，为TCP/IP连接提供了数据加密、消息完整性确认等客户机/服务器认证机制。

 在一般的HTTP协议中，可以使用SSL协议对HTTP协议进行数据加密处理，加密后的HTTP协议将使用数据的传输更加安全。加密后的HTTP协议在Web上使用HTTPS访问。默认使用443端口。

## OpenSSL

如果需要在系统中使用SSL，则需要对Apache服务器进行配置，使用mod_ssl模块能够运行。并且在相应的SSL配置文件中指定服务器要使用的证书文件。OpenSSL就是一款专门生成SSL证书文件的软件。

### mod_ssl模块的配置

mod_ssl模块是Apache服务器专门用来支持SSL协议的模块，该模块从Apache2开始随发行包同时发行，但是在默认情况下，该功能并没有被激活，配置该功能并使其在服务器上可用，可以通过以下步骤来完成。

- 用文本编辑器打开Apache安装目录下的conf文件夹下的httpd.conf
- 找到mod_ssl.so文件的所在行，并将前面的注释标识去掉

```
 LoadModule ssl_module modules/mod_ssl.so
```

- 找到包含httpd-ssl.conf配置文件的所在行，并将前面的注释标识去掉

```
Include conf/extra/httpd-ssl.conf
```

- 用文件编辑器打开extra文件夹下的httpd-ssl.conf文件，确保下面的代码可以在该文件中找到

```
Listen 445
```
