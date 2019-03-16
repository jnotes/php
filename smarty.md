# Smarty

Smarty是一款浒的模板引擎类库。所谓的模板引擎，就是一个用于执行PHP和模板页面的中间件。Smarty类库使用了先编译后执行的机制。如果在页面被访问以后，Smarty将直接调用编译过的PHP文件并将其输出。

使用模板引擎开发网站主要有以下两点好处:

- 高效
- 易维护

## Smarty配置

Smarty要求至少在以下三个文件夹以供Smarty运行时使用:

- configs: 用于存储配置信息
- templates: 用于存放模板
- templates_c: 用于存放编译后的PHP文件

## Smarty对象属性的定义

模板所在的文件夹是可以放在其他位置，但是，必须对模板对象的属性进行重新赋值，常用的模板对象的属性包含以下几种:

- `$smarty->template_dir`: 模板所在的文件夹路径
- `$smarty->compile_dir`: 编译好的PHP文件存放路径
- `$smarty->config_dir`: 配置信息所在文件夹存放路径
- `$smarty->left_delimiter`: 模板文件的左标记
- `$smarty->right_delimiter`: 模板文件的右标记

## Smarty使用

Smarty的PHP程序编写主要有以下几步:
- 通过包含文件载入Smarty类库
- 定义Smarty模板对象
- 设定Smarty模板对象的参数
- 将程序中处理的变量通过`assign`方法替换模板中的变量
- 将替换好的页面通过`display`方法输出

### 变量

变量使用`$`开头，但是与PHP不同的是，模板中的变量需要用一对定界符来标识。默放情况下，这一些定界符是是`{}`

### 变量的修饰

Smarty提供了对变量进行修饰的方法，也就是可以通过格式化的方法对Smarty中的变量进行格式化输出，Smarty提供了在模板中进行格式化的方法，其语法格式如下:

```PHP
{$variable|format_function}
```

其中`$variable`为变量,`format_function`用于格式化的方法。

### 区域循环方法

Smarty提供了循环的功能，用于对数组中的每一个元素实现相同的操作。Smarty主要提供了`foreach`和`section`两种方法来实现循环

`foreach`的语法格式如下:

```PHP
{foreach key=key1 item=item1 from=$array1}
{$item1}
{/foreach}
```

其中，一对`foreach`标记一个循环区域，`key1`表示数组中的每一个键值，`item1`表示数组中的每一个元素，`$array1`表示传入的数组变量名称

Smarty中的另一种循环方法是用`section`来实现，其语法格式如下:

```PHP
{section name=section1 loop=$array1}
{$array1[section1]}
{/section}
```

其中，一对`section`标记一个循环区域，`section1`表示这个循环区域的名字，`$array1`表示传入的数组变量名称。

### 条件判断

Smarty模板中，也可以根椐变量的值进行条件判断。判断的方法是通过`if`语句来实现的，其语法格式如下:

```PHP
{if condition}

{else}

{/if}
```

其中`condition`是用条件判断的逻辑语句。

### 外部文件的载入

Smarty还可以包含其他文件，这里的其他文件包括其他静态HTML文件及其他模板文件。由于Smarty模板可以接收来自PHP代码的变量，一个模板文件还可以根据需要动态包含不同的文件。包含文件的语法格式如下:

```PHP
{include file=$filename variable=$value ...}
```

其中,`$filename`是要包含文件的文件名，`variable`和`$value`是用于替换被包含文件中关键字的变量设定
