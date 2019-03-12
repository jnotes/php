# PEAR、PECL应用

PEAR是`PHP Extension and Application Repository`的缩写，即PHP扩展与应用类库。主要作用就是将PHP项目开发过程中的一些常用功能编写成类库供用户方便地调用。

PECL是`PHP Extension Community Library`的缩写，即PHP扩展库。PECL可以看作是PEAR的一个组成部分，提供了与PEAR类似的功能。但是与PEAR不同的是PEAR的所有扩展都是用PHP代码编写的，PECL是C语言开发的，通常用于补充一些PHP难以完成的底层功能，往往需要重新编译或者在配置文件中设置后才能在用户自己的代码中使用。

## PEAR的安装

由于PEAR在PHP中广泛应用，在PHP的安装包里已经集成了PEAR组件。PEAR的安装非常简单，只需要在命令行下运行`http://pear.php.net/go-pear`文件即可。

```bash
$ php -r "readfile('http://pear.php.net/go-pear');" > go-pear

$ php go-pear
```

## PEAR的使用

### 查看已安装的PEAR包

查看当前服务器已经安装了哪些PEAR包可以通过以下命令:

```bash
$ pear list
```

### 查看PEAR包的详细信息

如果需要进一步查看某一个PEAR包的详细信息可以通过下面的命令:

```bash
$ pear info <pear-package-name>
```

这里`pear-package-name`指的是PEAR包的名称

### 安装PEAR包

安装一个PEAR包是通过下面的命令来实现的:

```bash
$ pear install [option] <pear-package-name>
```

这里`pear-package-name`指的是PEAR包的名称,`option`是一个可选项,表示安装时的一些安装选项。

### PEAR包升级

```bash
$ pear upgrade <pear-package-name>
```

这里`pear-package-name`指的是PEAR包的名称

### PEAR包的使用

PEAR包的使用非常简单，只需要在PHP脚本文件中包含PEAR包文件即可:

```PHP
require_once('fpdf.php');
```

## PECL安装

将编译好的dll文件拷贝到PHP的扩展目录下，并修改`php.ini`，在其中加入以下代码即可:

```ini
extension=<DLL filename>.dll
```

这里的DLL filename是编译好的dll文件。修改好以后，重新启动Apache即可以使用。
