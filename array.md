# 数组

数组是由若干个同类型变量组成的集合，在引用这些变量时可用同一个名称。数组中的每一个变量都叫做数组元素。数组可能是一维的也可以是多维的。所谓的多维数组可以理解成元素中包含数组的数组。

# 数组操作

## 创建

在PHP中使用array函数来创建一个数组，它接爱一定数量用逗号分隔的`key => value`参数，其中`key`可以是`integer`或者`string`类型，`value`可以是任何值。也可以使用如下代码创建一个数组:

```PHP
$array = ['key'=>'value','key2'=>'value2']
```

## 使用和更新

获取或设置数组中的值使用`$array['key']`这种形式,如果是多维数组使用`$array['key']['key']`,如果想获取所有的值可以遍历数组

## 遍历

`foreach`函数是PHP提供的一种遍历数组的简便方法。`foreach`仅能用于数组，当试图将其用于其他数组类型或者一个未初始化的变量时会产生错误。它有两种语法格式。

```PHP
foreach($array as $value){
   // code...
}
```
在每次循环中，当前单元的值被赋给`$value`并且数组内部的指针向前一步。

```PHP
foreach ($array as $key => $value) {
  // code...
}
```
在每次循环中，当前单元的键被赋给`$key`,值被赋给`$value`

## 数组的索引与值

所谓索引，就是数组键名的集合。在创建数组的时候，数组的索引也会被随之建立。创建数组时可以省略键名。默认键名以`0`开始，依次`+1`

如果要删除一个键名使用`unset`函数进行释放。

- 使用`array_keys`获取数组的所有键。

- 使用`array_values`获取数组的所有值。

## 排序

### `sort`

`sort`函数对数组中的值进行递增排序。当函数结束时数组单元将被从最低到最高重新安排。

`void sort(array $array [,int sort_flags])`

其中`$array`是要排序的数组。`sort_flags`表示排序行为，包括以下三种:

- `SORT_REGULAR`: 正常比较单元
- `SORT_NUMERIC`: 单元被作为数字来比较
- `SORT_STRING`: 单元被作为字符串来比较

### `rsort`

与`sort`函数相反。

### `array_multisort`

`array_multisort`函数用于对多个数组或多维数组进行排序。与`sort`和`rsort`函数不同的是`array_multisort`函数排序时保留原有的键值关联，即数组的键不会被重新分配，该函数的语法格式如：

`bool array_multisort(array $array [,arg [,sort_flags]])`

其中 `$array`是要排序的数组`arg`是表示排序标志，包括以下几种：

- `SORT_ASC`：按照最低到最高的顺序排序
- `SORT_DESC`：按照最高到最低的顺序排序
- `SORT_REGULAR`：正常比较单元
- `SORT_NUMERIC`：单元被作为数字来比较
- `SORT_STRING`：单元被作为字符串来比较

### `shuffle`

`shuffle`函数可以随机将数组打乱，得到一个元素与原数组内容相同，顺序不同的新数组。

## 查找

### 顺序查找

使用遍历的方式来比对元素中的值。

### 二分法查找

二分法查找是在数组中查找某个元素的一种效率较高的方法。但是二分法查找假想数组已经是排好序的，然后通过对数组元素的比较得到的结果。每次不成功的比较都会排除掉二分之一的数组元素。

```PHP
function search($array,$k,$low=0,$high=0){
  if(count($array)!=0 && $high ==0){
    $high = count($array)
  }
  if($low <= $high){
    $mid = intval(($low+$high)/2);
    if($array[$mid] == $k){
      return $mid;      
    }elseif ($k < $array[$mid]) {
      return search($array,$k,$low,$mid-1);
    }else{
      return search($array,$k,$mid+1,$high);
    }
  }
}
```

### 使用`array_search`函数进行查找

`array_search(value,array)`函数，其中`value`是要查找的值，`array`是要查找的数组。该函数如果在数组中找到了要查找的值，则返回该值所在的键，如果没有找到，则返回`false`.

### 线性表的入栈与出栈

#### 入栈

通过`array_push`函数入栈，其语法格式如下：

```PHP
int array_push(array,var [,var ...])
```

`var`为要入数组的元素，`array`为数组，函数将返回数组新的元素总数。`array_push`函数将在数组的未尾追加新元素。还可以使用`array_unshift`函数追加元素到数组的第一个元素前。

#### 出栈

通过`array_pop`函数来实现，该函数返回数组的最后一个元素，即被删除的元素。使用`array_shift`返回数组的第一个元素，并且第一个元素将被删除。

## 合并

通过`array_merge`函数用于合并数组。其语法格式如下：

```PHP
array_merge(array1,array2,...)
```

该函数将参数中的数组合并到一个数组中。

## 拆分

通过`array_slice`函数来拆分数组，其语法为:

```PHP
array_slice(array,int start [,int length])
```

这里`array`是原数组，`start`是子集的开始位置，`length`是子集的长度。如果不指定`length`则表示一直取到数组的未尾。

PHP提供了一种真正达到拆分数组的函数`array_splice`函数。该函数与`array_slice`用法完全相同，不同的是其结果会将取出的元素从原数组中删除。
