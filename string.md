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

字符串查找操作，在PHP中使用`strstr`和`stristr`函数进行字符串查找操作。`string strstr(string str,string search)`,这里的，`str`是要进行查找的字符串，`search`是要查找的内容。这个函数返回找到的第一个全匹配的位置以后的全部内容。`strstr`是大小写敏感的，`stristr`是大小写不敏感的。

### `strlen`

获取字符串长度，`int strlen(string str)`

### `substr`

获取子字符串，在实际应用中，通常需要截取某一段字符串，`substr`函数用来截取一部分字符串，其语法格式是`string substr(string str,int start [, int length])`，这里的`str`是要进行截取的字符串，`start`是开始字符位置，`length`是要截取的长度，如果不指定`length`，则默认为截取到字符串未尾。

## 正则表达式

正则表达式是描述字符串集的字符串。例如，正则表达式`*PHP*`描述所有包含`PHP`并且前面或后面跟零个或多个字符的字符串。如：`PHPMyadmin`、`MyPHP`、`ZendPHPFramework`或`PHP`本身。`.`匹配任何字符，`+`类似`*`，但至少要一个字符，`[a-z]`指一个匹配范围，所以`[a-zA-Z_0-9]`匹配字母、数字、下划线，也可以将它写成`\w`。`\w+`匹配至少有一个字符的单词序列。例如，正则表达式`^[a-zA-Z_]\w*$`。专用字符`^`的意思是"以...开始"，`$`的意思是"结尾"。正则表达式在对输入进行有效性验证时非常有用。在`PHP`中正则表达式的函数规定表达式必须被包含在定界符中，如使用`/`作为定界符。

### `preg_grep`

`preg_grep`函数用来获得与模式匹配的数组单元。`array preg_grep(string pattern,array input)`,`pattern`是用来匹配的正则表达式，`input`是用来匹配的数组。需要注意的是`preg_grep`函数返回的结果使用从输入数组来的键名进行索引。

### `preg_match_all`

`preg_match_all`函数用来进行全局正则表达式的匹配，`int preg_match_all(string pattern,string input,array matches)`。`pattern`是用来匹配的正则表达式，`input`是用来匹配的字符串,`matches`是匹配结果的数组。

### `preg_match`

`preg_match`函数用来进行正则表达式匹配。与`preg_match_all`函数不同，`preg_match`函数在第一次匹配后将停止搜索。`int preg_match(string pattern,string input,array matches)`。`pattern`是用来匹配的正则表达式，`input`是用来匹配的字符串,`matches`是匹配结果的数组。

### `preg_quote`

`preg_quote`函数用来进行正则表达式的转义。`preg_quote`函数用于将字符串中所有具有正则表达式意义的字符进行转义。在实际应用中，如果需要用动态生成的字符串来作为正则表达式进行模式匹配，则可以用此函数转义其中可能包含的一些特殊字符。这些特殊字符包括：`.`,'\\','+','*','?','[]','^','$','()','{}','=','!','<>','|',':'等。 `string preg_quote(string str[, string delimiter])`。这里参数`str`是用来进行字符串转义的正则表达式，`delimiter`是其他需要转义的字符。

### `preg_replace`

`preg_replace`与前面的`preg_match`函数的使用方法类似，但是还是提供了字符串的替换功能，`preg_replace(pattern,replacement,subject [,int limit])`，参数`pattern`是进行匹配的正则表达式，`replacement`是要将匹配部分替换成的字符串或者正则表达式，`subject`是要被匹配的字符串，`limit`是要进行的匹配次数。

### `preg_replace_callback`

`preg_replace_callback`的用法几乎和`preg_replace`函数一样。但是，使用`preg_replace_callback`函数可以获得比`preg_replace`更完善的替换功能。`preg_replace`的替换只是基本的字符串间的计算，而`preg_replace_callback`函数可以将要替换的字符串传入到一个函数中进行处理，并将处理后的结果进行替换。`preg_replace_callback(pattern,callback,subject [,int limit])` 。参数`callback`是一个函数。

### `preg_split`

`preg_split`提供了用正则表达式分割字符串的功能，`array preg_split(string pattern,string subject [, int limit])`
