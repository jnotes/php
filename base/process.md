# 流程控制

在程序编写中，还可以用花括号将一组语句封装成一个语句组。一个常见的PHP脚本就是由一系列语句或者语句组构成的。

## 条件控制语句

### if

```PHP
if (condition){
  // code...
}
```

### if...else

```PHP
if (condition) {
  // code...
} else {
  // code...
}
```

### if...elseif...else

```PHP
if (condition) {
  // code...
} elseif(condition){
  // code...
} else {
  // code...
}
```

### switch

```PHP
switch (variable) {
  case 'value':
    // code...
    break;

  default:
    // code...
    break;
}
```

## 循环控制语句

### while

```PHP
while ($a <= 10) {
  // code...
}
```

### do...while

```PHP
do {
  // code...
} while ($a <= 10);
```

### for

```PHP
for ($i=0; $i < 10; $i++) {
  // code...
}
```

### foreach

```PHP
foreach ($variable as $key => $value) {
  // code...
}
```

## 转移控制语句

### break

用于结束当前循环结构`for`、`foreach`、`while`、`do`...`while`或者`switch`的执行。

### continue

在循环结构中用于跳过本次循环中剩余代码，并开始执行下一次循环。

### return

用于结束一个函数或一个脚本文件。如果在函数中使用将立即结束此函数的执行，并将它的参数作为函数的值返回。在全局范围中，则当前脚本文件中止运行。
