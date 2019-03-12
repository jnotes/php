# FPDF

## 创建PDF

创建PDF的语法格式如下:

```PHP
$pdf = new FPDF([string page-orientation [, string measure-unit [, string page-format]]]);
```

其中，`page-orientation`用于表示创建的PDF文件是横向还是坚向的。可用的值有以下两种:

- P: 竖向
- L: 横向

`measure-unit`用于表示文档中位置的计量单元。可用的值有以下四种:

- pt: 点
- mm: 毫米
- cm: 厘米
- in: 英寸

`page-format`用于表示创建的PDF文档的纸张类型。可用值可以是用于表示纸的字符串，如"A4"、"A5"、"Letter"等，也可以是一个包含两个无素的二维数组.

```PHP
$pdf->Open()
```

Open函数用于开始创建PDF文档

```PHP
$pdf->AddPage([string page-orientation])
```

用于添加一个新页

```PHP
$pdf->SetFont(string font [,string style [, float size]])
```

用于设置字体，其中font用于表示字体，style用于表示样式，style可用值可以是以下三种:

- B: 粗体
- I: 斜体
- U: 下划线

size用于表示字体的大小。默认值为"12pt"

```PHP
$pdf->Cell(float width,float height,string str,int bolder)
```

增加一个单元格，其中width表示增加单元格的宽度，height表示增加的单元格的高度，str表示要放置在单元格中的字符串，bolder表示单元格的边框。如果将width或height设置为0，表示该单元格不存在。

```PHP
$pdf->Output([string filename [, bool download]])
```

输出PDF文档，filename表示要存储的文件名。如果不指定文件名，浏览器会直接打开。download表示是否一定要用户下载查看，默认为`false`

## 插入图片

使用Image函数向PDF插入图片，其语法格式如下:

```PHP
$pdf->Image(string file,float x,float y,float width,float height)
```

其中`x`和`y`表示图片所在的坐标，`width`和`height`表示图片的宽度和高度。如果需要图片保持原来的大小，只需要将`width`和`height`设置成`0`即可。

## 页眉与页脚

页眉与页脚是通过重写FPDF类中的`Header`方法和`Footer`方法来实现的。在原有的FPDF类中存在这两个方法，但是方法体没有任何内容，在输出PDF文档时，这两个方法将被自动调用。在页眉与页脚中用的方法`PageNo()`其语法格式如下:

```PHP
$pdf->PageNo();
```

该方法返回当前页码。

```PHP
require_once('fpdf/fpdf.php');

class PDF extends FPDF{
  function Header(){

  }

  function Footer(){

  }
}

```

在设置页脚的时候，方法`SetY`是必不可少的，其语法格式如下:

```PHP
$this->SetY(float y);
```

这里的`y`指代页面上的Y坐标。单位为毫米，如果`y`为负数，则表示从页面底部向上的距离。
