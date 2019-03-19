# MAIL

## 配置

要使用PHP发送邮件，首先需要配置SMTP服务器。SMTP是“简单邮件传输协议(Simple Mail Transfer Protocol)”的缩写，是一种可靠并且有效的电子邮件传输协议。使用PHP发送邮件的原理也正是通过SMTP服务器将E-Mail发送到指定地址。

打开PHP安装目录下的php.ini文件：

```ini
[mail function]

SMTP=localhost
smtp_port = 25
```

可以看到这里需要配置在发送邮件时使用的SMTP服务器地址和SMTP服务器所用的端口。

## PHP中的mail函数

PHP提供了一个功能强大的`mail`函数用于发送邮件，可以通过`mail`函数来实现各种类型的邮件发送。

### 简单的邮件发送方法

`mail`函数的语法格式如下:

```PHP
mail($to,$subject,$body,[$header])
```

其中,`$to`是收件人的E-mail地址，如果存在多个收件人，则将地址用逗号`,`分开。`$subject`是邮件的标题，`$body`是邮件的主体部分，`$header`是一个可选项，用于表示邮件的头信息。如下:

```PHP
MIME-Version: 1.0 //邮件协议版本信息
Content-type: text/html; charset=utf8 //数据类型和字符集
To: Simon <test@tes.com>, Eld <eld@test.com> //收件人
From: Sender <fdsaf@test.com> //发件人
Cc: 1@test.com //抄送地十
Bcc: 2@test.com //暗抄地址
```

### 发送HTML格式邮件

在邮件的头信息中指定MIME的类型为HTML后，可以使邮件的内容按照HTML格式发送

### 发送带附件的邮件

除了HTML邮件可以通过设置Header的方式发送外，其他的文件也可以通过这种形式发出。如果一个E-Mail包含多种MIME类型，例如即有图片又有文本，那么可以在头信息中指定一个MIME类型分界线，然后在邮件的主体部分声明MIME类型，并用分界线隔开。

以下代码在头信息中构建一个分界线:

```
$header = "Content-type: multipart/mixed; boundary= 3465673123213 \r\n";
```

这里的`boundary`就是分界线，分界线是一串无规律的字符。定义分界线时，MIME类型指指定为`multipart/mixed`
