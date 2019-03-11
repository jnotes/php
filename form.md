# 表单

## 表单数据的接收

### `GET`

如果是`GET`请求，表单和URL的数据都会在`$_GET`数组中。

### `POST`

如果是`POST`请求，表单中的数据会在`$_POST`数组中，URL的数据会在`$_GET`数组中。

### 文件上传

#### 表单设置

如果需要上传文件，需要设置`FORM`为`enctype="multipart/form-data"`

#### 收接文件

PHP在收接上传文件，会把上传的文件放在`$_FILE`数组中。

## 表单数据的验证

### `ereg`

通过`ereg`函数可以验证表单提交的数据，`ereg`函数形式如下：

```PHP
bool ereg(string pattern,string str);
```

其中，`pattern`是正则表达式，`str`是要被匹配的字符串。

## URL编码解码函数

### `urlencode`


### `urldecode`
