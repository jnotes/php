# 基础语法

PHP文件以反缀为.php为结尾，在此文件中以`<?php`开始`?>`结束。通常`?>`可省略。

PHP要求每条语句必须以分号`;`结尾，一个完整的php语句通过由一个或多个表达式构成。表达式用来完成一些基本的运算操作。通过把常量，变量和运算符等基本元素连接起来得到一个运算结果代其他函数或表达式使用。

## 注释

- 单行注释 `//` 或 `#`
- 多行注释 `/*.....*/`

## 当前PHP信息

> phpinfo() 函数可以查看当前服务器的配置信息

### php.ini

`php.ini`文件包括以下部分

- 语言选项（Language Options）
- 安全模式（Safe Mode）
- 语法高亮（Syntax Highlighting）
- 杂项（Miscellaneous）
- 资源限制（Resource Limits）
- 错误处理与日志（Error Handling and Logging）
- 数据处理（Data Handling）
- 路径与目录（Paths and Directories）
- 文件上传（File Uploads）
- 文件包装（Fopen Wrappers）
- 动态扩展（Dynamic Extensions）
- 模块设定（Module Settings）

### php.ini 的常用参数

#### max_execution_time

每个脚本的最大执行时间，单位为秒。如果脚本在规定时间内没有执行完成，脚本将非常结束。

#### memory_limit

脚本最大可使用的内存总量，单位为字节。如果脚本占用的内存资源超过了这个限制，脚本将非常结束。

#### display_errors

是否输出错误信息。如果设置为On,则一旦脚本出错，错误信息将作为输出的一部分输出到屏幕上。

#### file_uploads

是否允许通过HTTP方式上传文件

#### allow_url_fopen

是否允许通过读写文件的方式读写远程HTTP文件

#### extension

指定加载PHP扩展
