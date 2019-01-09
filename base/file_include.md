# 文件包含

### `require` 和 `require_once` 、`include` 和 `include_once`

#### `require` 、 `include`

`require`、`include` 语句用于将指定的文件包含到代码本身

#### `require_once` 、`include_once`

`require_once`、`include_once` 能够自动检测文件是否已经被包含，由此避免可能的重定义错误。

### `require` 和 `include` 对比

> 功能和使用方法上相同

#### 机制不同

- `require` 语句在进行文件包含时，不管这条`require` 语句是否被运行，都会将被包含的代码包含进来。
- `include` 语句在进行文件包含时，如果这条`include` 语句没有被运行，则被包含文件的代码不会包含进来。​

#### 文件不存时的错误处理方式不同

如果被包含的文件无法找到，`require`语句与`include`语句的错误提示是不相同的。`require`语句会抛出一个致命错误并中止脚本运行。而`include`只会抛出警告信息。
