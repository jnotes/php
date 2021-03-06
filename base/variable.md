# 变量与常量

## 常量

### 定义

常量是一个不能改变的量，在脚本执行期间常量的值不能改变。常量默认为大小写敏感，使用大写字母字义的常量名不能用小写字母来调用。常量可以用`define`函数来定义。一个常量一量被定义，就不能再改变或者取消定义。

### 声明

```PHP
bool define(string name,value [,bool case_insensitive])​;
```

- `name`指常量名
- `value`指常量的值,常量的值必须是标量，也就是专门用于表示一个特定值的量。
- `case_insensitive`表示常量名是否为大小写敏感，如果为`TRUE`，则表示常量名是大小写不敏感的。

### 使用

#### 判断是否已经存在

```PHP
bool defined(string name);
```

> 判断常量是否定义，返回`TRUE`或`FALSE`

#### 获取已存在的常量

```PHP
Array get_defined_constants();
```

> 获取所有已经定义的常量，返回数组

## 魔术常量

### `__LINE__`

文件中的当前行号

### `__FILE__`

文件的完整路径（绝对路径）和文件名。

### `__DIR__`

文件所在的目录

### `__FUNCTION__`

函数名称 在函数中使用

### `__CLASS__`

类的名称，在trait中返回的trait名称

### `__TRAIT__`

trait名称

### `__METHOD__`

方法名称

### `__NAMESPACE__`

当前命名空间的名称

## 变量

### 定义

变量是用来临时存储值的量。在PHP中，用一个`$`符号后面跟上一个变量名表示一个变量。如`$var`，变量名是大小写敏感的。在指定变量的时候，没有大小写敏感选项。

PHP中的变量不需要先定义后使用。在变量第一次使用的时候，变量被自动定义。需要注意的是类中的变量需要先定义。PHP提供两种方式对变量进行赋值，传值赋值和传地址赋值。

- 使用传值赋值时，整个原始表达式的值将被复制给目标变量。这时改变原始表达式时，目标变量的值将不会被影响。
- 使用传地址赋值时，目标变量简单引用了原始变量。改动目标变量将影响到原始变量，反之亦然。传地址赋值通过在要赋值的变量前追加一个`&`符号来完成。如$a=&$b，将变量$b以传地址赋值的方式传递给$a

### 声明

```PHP
$var = 'Hello World!';
```

> 声明一个变量，值为`Hello World!`

### 作用域

> 变量的作用域指的是变量定义的生效范围。大部分的PHP变量只有一个单独的范围。这个单独的范围跨度同样包含了引入的文件。

#### 本地变量

默认情况下，任何用于函数内部的变量都被限制在局部函数范围内。

#### 全局变量

任何可以用于全部PHP脚本的变量被称为全局变量。PHP提两种定义全局变量的方法​

##### 使用global关键字

```PHP
$a = 1;
function func(){
    global $a;
    echo $a;​
​​}​
func();​
```

##### 使用$GLOBALS数组

```PHP
$a = 1;
function func(){
   echo $GLOBAL["a"];
​​}​
func();​
```

#### 静态变量

静态变量仅在局部函数中存在，但当程序执行离开此函数时，并值并不丢失。

```PHP
function func(){
   static $a = 1;
   echo $a;
   $a++;​​
​​}​
func();
func();​​​​
```

#### 动态变量

动态变量的变量名是可变的，也就是通过另一个变量传递的。对于这种变量，使用两个`$`进行定义。

```PHP
$var_name = "ic";
$$var_name = "Simon";
echo $var_name;
echo $$var_name;
echo $ic;​​​​​​
```
