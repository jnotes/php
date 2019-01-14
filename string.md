# 字符串处理

## 字符

字符串是由字符组成的，字符包括以下几种类型

- 数字
- 字母
- 特殊字符
- 不可见字符
不可见字符是比较特殊的一组字符，是用来控制字符串格式化输出的，并不能在屏幕上看到字符本身，而只能看到字符带来的一些结果。​

### 字符的显示

字符的显示主要分为两种方式，使用`print`和`echo`进行输出。`print`是一个类似于函数的输出方式，但是`print`并不是一个真正意义上的函数。`echo`支持多参数，`print`不支持，两个字符串连接使用"."符号。

### 字符的格式化

​​使用`sprintf`函数对字符串进行格式化操作。

`string sprintf(string format,str1,str2)`

`format`是要输出的字符串格式，`str1`,`str2`等是要格式化输出的其他字符串，`format`字符串中的格式由一般的字符和一些以`%`号开头的字符构成，这些以`%`开头的字符用来指代后面的参数。这些字符包括以下几种。​​

- `%b` 参数将被认为是整型数，并且以二进制形式输出。
- `%c` 参数将被认为是整型数，并且以ASCII码形式输出。
- `%d` 参数将被认为是整型数，并且以有符号数形式输出。
- `%u` 参数将被认为是整型数，并且以无符号数形式输出。
- `%o` 参数将被认为是整型数，并且以八进制形式输出。
- `%x` 参数将被认为是整型数，并且以十六进制数形式输出，其中的字母为小写形式。
- `%X` 参数将被认为是整型数，并且以十六进制数形式输出，其中的字母为大写形式。
- `%f` 参数将被认为是浮点数。
- `%s` 参数将被认为是字符串。

## 字符的操作

### `str_repeat`

字符串重复操作,`string str_repeat(string input,int multiplier)`,这里的`input`参数表示的是要重复的字符串，`multiplier`表示的是重复的次数。

### `str_replace`和`str_ireplace`

字符串替换

#### `str_replace`

`string str_replace(search,replace,subject [,int count])`，这里`subject`是要进行替换的字符串，`search`是查找内容，`replace`是要替换成的内容，`count`用来接收替换的次数。

#### `str_ireplace`

`str_ireplace`函数的用途非常广泛，尤其是在搜索引擎和模板式网站系统中。但是`str_replace`有一个很大的不足就是大小写敏感。因此在如果要实现大小写不敏感的替换信息时就会非常麻烦。`str_ireplace`和`str_replace`的区别是`str_ireplace`对大小写不敏感。

### `str_split`

字符串分解操作，`array str_split(string str [, int split_length])`这里,`str`是要进行分解的字符串，`split_length`是分解的长度，也就是每小段有多长，如果不指定`split_length`，就默认为`1`。

### `str_word_count`

字符串单词数的计算函数，`str_word_count(string str [, int format])`这里，`str`是要进行分解或者计算的字符串，`format`包括以下两种，如果没有`format`返回单词数量。`format`为`1`，返回一个包含`str`中全部单词的数组，数组的键值按照顺序排列。​`format`为`2`，返回一个包含`str`中全部单词的数组，数组的键值反映了单词所在的位置。​

### `strstr`

### `strlen`

### `substr`

## 正则表达式
