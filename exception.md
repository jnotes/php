# 异常处理

## 异常处理的原理

PHP中的异常处理是PHP5新引进的一项功能，与其他语言类似，在PHP中进行异常处理也是用关键字`try`、`catch`和`throw`来实现的。其中`try`的功能是检测异常，`catch`的功能是捕获异常，`throw`的功能是抛出异常。

## PHP中的异常处理

`try`关键字必须与`catch`关键字对应，一个`try`关键字可以与多个`catch`关键字相对应以捕获不同的异常。PHP程序会按所有与`try`关键字相对应的`catch`关键字定义的顺序执行，直到所有的异常均被检测完成。

对于抛出的异常，除了可以用`catch`捕获以外，还可以使用`set_exception_handler`函数进行处理。如果一个异常即没有被捕获，也没有使用`set_exception_handler`函数进行处理，将会产生一个严重的错误。

### 异常类`Exception`

`Exception`类用于脚本发生异常时建立异常对象，该对象将用于存储异常信息并用于抛出和捕获。在准备抛出异常时，需要首先建立异常对象，其语法格式如下：

```PHP
$e = new Exception([string $msg [,int $code]]);

echo $e->getMessage();
```

### 异常抛出关键字`throw`

异常对象是由`throw`关键字抛出的，其语法格式如下:

```PHP
throw new Exception();
```

### 异常捕获语句`try-catch`

一个`try`语句至少和一个`catch`语句相对应。`try-catch`语句的语法格式如下：

```PHP
try{
  throw new Exception("Error Processing Request", 1);
}catch(Exception $e){
  // 捕获异常后的操作
}
```

### 异常处理函数设置`set_exception_handler`

有些时候，使用一个专门的函数对一些可能没有被捕获的异常进行处理。这个函数可以通过`set_exception_handler`来设置，其语法格式如下:

```PHP
set_exception_handler(exception_handler)
```

其中`exception_handler`是用于处理未捕获异常的函数名。需要注意的是用于处理未捕获异常的函数必需用`set_exception_handler`前定义。

```PHP
function exception_handler($e){

}
```

其中，`$e`是异常对象。

### 完整的异常信息

在实际应用中，往往会根据要显示出更详细的异常信息。这时，就需要使用`Exception`类中的其他方法。`getTrace`函数返回一个用于储存跟踪路线的数组，主要包含以下键值：

- file: 发生异常的程序文件名。
- line: 发生异常的代码所在的行号
- function: 发生异常的函数或方法
- class: 发生异常的函数或方法所在的类
- type: 调用发生异常的函数或方法的类型
- args: 发生异常的函数或方法所接受的参数

## 扩展的异常处理类

在实际应用中，往往根据异常类型的不同使用不同的异常处理类。这就需要对一般的异常处理类`Exception`进行扩展。对`Exception`类进行扩展有以下三点好处：
- 提高代码的可读性，容易区别不同类型的异常。
- 扩展类可以提供自定义功能。
- 捕获异常时可根据异常类型的不同做出不同的反应。

一个类继续自`Exception`即可扩展异常类。

在捕获异常时分别捕获不同的异常对象来获得不同的信息，需要注意以下两点：
- 捕获异常时，往往仍然需要捕获`Exception`类，以用来处理未捕获的异常
- 在捕获时是按照从上向下的捕获顺序，如果先捕获`Exception`类，则会导致异常不能被正确的代码处理。所以，应当异常子类写在前面，父类写在后面。
