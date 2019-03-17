# GD

PHP中使用GB库来对图像进行操作，GD库是一个开放的动态创建图像的源代码公开函数库。GD库使用C语言开发，可以在Perl等多种程序语言中调用。目前的GD库支持PNG、JPEG和GIF等多种图像格式。GD库通常用于创建图片、文字及对其他的图片进行处理。

## 配置

GD库是PHP5中是被默认安装的，但是要想激活GD库，必须修改PHP安装路径下的php.ini文件使其增加GD库的扩展

```ini
extension=php_gd2.dll
```

修改好php.ini文件后重启Apache服务器即可使改动生效。

GD库提供了一个函数`gd_info`来显示GD库的安装信息，其语法格式如下:

```PHP
array gd_info();
```

该函数返回一个包含有完整GD安装信息的数组。

## 创建图片

```PHP
header("Content-type: image/png");
$image = imagecreatetruecolor(200,100);
$text_color = imagecolorallocate($image,255,255,255);
imagestring($image,5,0,0,"Hello World!",$text_color);
imagepng($image);
imagedestroy($image);
```

- `header("Content-type: image/png")`用于声明当前图片的格式
- `imagecreatetruecolor`函数用于创建一个真彩包的空白图像，其语法格式如下:

```PHP
imagecreatetruecolor(int x,int y);
```

其中`x`为图片的宽,`y`为图片的高，该函数返回一个图像资源。

- `imagecolorallocate`函数用于确定当前的颜色设置，其语法格式如下:

```PHP
imagecolorallocate($image,int red,int green,int blue);
```

其中`$image`为前面创建的图像对象，`red`、`green`、`blue`为用于确定三种颜色的值。

- `imagestring`函数用于水平输出一行字符串，其语法格式如下:

```PHP
imagestring($image,int font,int x,int y, string str,int color);
```
其中`$image`为前面创建的图像对象，`font`是所用的字体，`x`、`y`是字符串所在图像的坐标,`str`是要输出的字符串，`color`是前面设置的颜色。

## 创建缩略图

`ImageCreateFromJPEG`是一个用于从图片文件创建图片对象的函数，其语法格式如下:

```PHP
ImageCreateFromJPEG($filename)
```

其中`$filename`是源文件名。类似的函数还包括以下几个:

- `imagecreatefromdg2`: 从GD2文件或URL新建图像
- `imagecreatefromdg`: 从GD文件或URL新建图像
- `imagecreatefromgif`: 从GIF文件或URL新建图像
- `imagecreatefromjpeg`: 从JPEG文件或URL新建图像
- `imagecreatefrompng`: 从PNG文件或URL新建图像
- `imagecreatefromstring`: 从字符串中的图像流新建图像
- `imagecreatefromwbmp`: 从WBMP文件或URL新建图像
- `imagecreatefromxbm`: 从XBM文件或URL新建图像
- `imagecreatefromxpm`: 从XPM文件或URL新建图像

`ImageSX`和`ImageSY`分别用于获得图像的宽与高，其语法格式如下:

```PHP
Int ImageSX($image)
Int ImageSY($image)
```

其中`$image`是已经创建好的图像对象。

`ImageCopyResized`函数用于读取源图像的全部或部分并调整大小，其语法格式如下:

```PHP
int imagecopyresized(dst_im,src_im,int dstX,int dstY,int srcX,int srcY,int dstW,int dstH,int srcW,int srcH)
```

其中`dst_im`是目标图像对象，`src_im`是源图像对象，`dstX`和`dstY`分别表示目标图像所在的坐标，`srcX`和`srcY`分别表示源图像坐标，`dstW`和`dstH`分别表示目标图像的宽和高，`srcW`和`srcH`分别表示源图像的宽和高。

`ImageJpeg`函数用于创建一个新的JPEG图像。

## 增加水印

`ImageCopy`函数用于合并两个图像。
