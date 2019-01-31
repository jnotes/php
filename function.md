# 函数处理

## 函数的调用

调用函数的方法非常简单，只需要按照函数格式写出函数及其相应的参数即可。
如: `substr("This is a test",8);`

## 函数的定义

一个函数通常由四部分组成，函数名，参数，函数体和返回值

```PHP
function func($arg1,$arg2){
  return $arg1+$arg2;
​​}
```

​任何有效的PHP代码都有可能出现在函数内部，甚至包括其他函数的定义​函数名是非大小写敏感的，但在调用函数的时候，通常使用与期定义时相同的形式。​​函数定义可以在调用之前，也可以在调用之后。但是如果函数的定义在条件结构之内，或者在其他函数之内，则函数的定义必须在函数调用之前被运行到。

## 常用函数

### `getdate`

获得当前时间，或者用来分析时间戳的具体意义。返回一个数组，包括日期和时间的完整信息。精确到秒

### `gettimeofday`

返回当前的日期时间的详细信息。精确到微秒

### `checkdate`

验证一个日期是否有效

### `date`

格式化本地日期时间

### `mktime`

对日期和时间计算一个本地化的时间戳。

### `flush`

输出缓存区。

### `isset`

检测变量是否已经被赋值

### `unset`

销毁指定的变量

### `rand`

用来生产一个随机数，rand是一种伪随机数

### `srand`

用来生产一个随机数，支持用户自定义随机数发生器


## 魔术函数

### `__construct()`

构造函数，对象初始化时执行此方法

### `__destruct()`

析构函数，对象销毁时执行此方法

### `__get()`

获取对象不存在的属性或无法访问的属性时调用.

### `__set()`

设置对象不存在的属性或无法访问的属性时调用.

### `__isset()`

当调用方法isset()方法判断不可访问的类属性时调用.

### `__unset()`

当调用方法unset()方法删除不可访问的类属性时调用.

### `__call()`

调用对象方法不存在或不允许被调用时此方法会被调用

### `__callStatic()`

调用对象的静态方法不存在或不允许被调用时此方法会被调用

### `__sleep()`

当调用searialize()方法时调用，返回值为数组，表示需要序列化的数据项.

### `__wakeup()`

当调用unsearizlie()方法时调用。一般用来在唤醒时初始化资源对象

### `__toString()`

当对象在需要转换成字符串时，会调用此方法

### `__clone`

此方法在复制对象时被调用clone $obj​

### `__autoload()`

主要用来自动加载类。那如何自动加载呢？我们都知道在php中，要使用另外一个文件中的类需要用`require`或`include`方法(包括`require_once`和`include_one`)导入进来。那么如果我要使用的类未被导入，则引擎会自动调用`__autoload()`方法。利用此特性，当我们的类名和类文件有规律地存放时，我们可以使用`__autoload()`方法，根据需导入的类名，让程序自动导入文件

### `__set_state()`

自 PHP 5.1.0 起当调用 var_export() 导出类时，此静态 方法会被调用。

### `__invoke()`

把对象当方法用的时候。此方法会被调用

## 引用的解释

使用`&`符号进行的传地址赋值实际上就是对变量的一种引用方法。

### 变量的引用

对变量的引用即使两个变量来指代一个内容，这些非引用的直接赋值是完全不同的，这种对变量的引用还可以用于函数的参数变量。`$a = 0;$b = &$a;function func(&$a){​}​​​​`

- `$this` 在对象中，永远指向对象自身的引用
- `parent` 在对象中，永远指向父对象的引用

### 函数的引用

对函数的引用，用来实现对函数返回结果的引用。在使用函数的引用方法时，在函数名前加上`&`符号`function &func(){​}​`

### 引用的释放

释放一个引用也是通过unset函数来实现，但是与释放变量不同的是，释放引用并不会消除引用中的值，只会消除引用的变量名。