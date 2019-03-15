# XML

XML是“可扩展性标识语言（Extensible Markup Language）”的缩写，是一种类似于HTML的标记性语言。

XML是一种“元标记”语言，开发者可以根据自己的需要创建标记名称。

在XML文件的顶部，通常使用`<?xml version="1.0"?>`来标识XML数据的开始和XML数据使用的版本信息

## XML操作

PHP与XML的交互操作应用非常广泛。`SimpleXML`缓件是PHP5新增加的一个简单的XML操作组件，与传统的XML组件相比，`SimpleXML`组件使用更加简单。

### 创建`SimpleXML`对象

`SimpleXML`对象是用来临时存储XML数据的临时变量，对XML进行的操作都是通过操作`SimpleXML`对象来完成的。`SimpleXML`组件提供了两种创建`SimpleXML`对象的方法。

第一种方法是使用`simplexml_load_string`函数读取一个字符串变量中的XML数据来完成创建，其语法格式如下:

```PHP
simplexml_load_string(string $data)
```

这里的`$data`变量用于存储XML数据字符串。

第二种方法是使用`simplexml_load_file`函数读取一个XML文件来完成创建，其语法格式如下:

```PHP
simplexml_load_file(string $filename)
```

这里的`$filename`变量用于存储XML数据文件的文件名及其所在的路径。

### 读取`SimpleXML`对象中的标签数据

与操作数组类型的变量类似，读取XML也可以通过类似的方法来完成。如：

```PHP
$xml = simplexml_load_file('example.xml');

foreach ($xml->root as $key => $value) {
  echo $value->name;
}

//or

echo $xml->root->name[0];

//or

foreach ($xml->root->children() as $key => $value) {
  var_dump($value);
}

```

### 基于XML数据路径查询

`SimpleXML`组件提供了一种基于XML数据路径的查询方法。XML数据路径即从XML的根到某一个标签所经过的全部标签。这种路径使用`/`隔开。如:`/root/depart/name`

`SimpleXML`组件使用`xpath`方法来解析路径。其语法格式如下：

```PHP
$xml->xpath(string path);
```

其中的`path`为路径。该方法返回了一个包含所有要查询的标签值的数组。

### 修改XML数据

XML数据的修改与读取XML数据中的标签方法类似。即通过直接修改`SimpleXML`对象中的标签的值来实现。

```PHP
$xml->root->name[0] = "Hello World!";
```

修改后，不会对XML文件有任何影响，只是对`SimpleXML`对象的读取将使用新值。

### 标准化XML数据

`SimpleXML`还提供了一种标准化XML数据的方法`asXML`。可以有效地将`SimpleXML`对象中的内容按照XML 1.0标准进行重新编排并以字符串的数据类型返回。

```PHP
echo $xml->asXML();
```

### XML数据的存储

```PHP
$newxml = $xml->asXML();
$f = fopen("newxml.xml","w");
fwrite($f,$newxml);
fclose($f);
```

## XML文档的动态创建

在实际应用中，有时会需要动态生成XML文档。前面介绍的`SimpleXML`组件并不提供创建XML文档的方法。因此，如果需要动态创建XML文档，往往需要使用DOM组件进行创建。

```PHP
$dom = new DOMDocument();
$root = $dom->createElement('root');
$dom->appendChild($root);

echo $dom->saveXML();
```
