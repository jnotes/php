# 加速器

PHP代码在运行时首选是通过编译器编译成中间代码，然后再被服务器运行得到用户所需要的结果。因此，中间代码的优劣直接决定了整个PHP代码的最终运行速度。目前，有一些常见的PHP加速器可以通过对中间代码进行优化来提高PHP代码的运行速度。

## Zend Optimizer

Zend Optimizer是PHP的开发商Zend公司开发的官方PHP加速器，其优化效果非常明显。

## Zend Optimizer 配置

Zend Optimizer的配置可通过修改php.ini来实现，主要的配置参数有两项。如果需要修改某个参数，可以直接在php.ini中声明

- zend_optimizer.encoder_loader

该参数用于声明是否处理由Zend Encoder加密的PHP文件，0表示不允许，1表示允许

- zend_optimizer.optimization_level

该参数用于声明优化程度，也就是启动的优化进程数。在Zend Optimizer中包含10个优化进程，每个优化进程的对应代码如下表：

|优化进程名称|对应代码|
|--|--|
|不使用|0|
|优化进程1(Optimization Pass 1)|1|
|优化进程2(Optimization Pass 2)|2|
|优化进程3(Optimization Pass 3)|4|
|优化进程4(Optimization Pass 4)|8|
|优化进程5(Optimization Pass 5)|16|
|优化进程6(Optimization Pass 6)|32|
|优化进程7(Optimization Pass 7)|64|
|优化进程8(Optimization Pass 8)|128|
|优化进程9(Optimization Pass 9)|256|
|优化进程10(Optimization Pass 10)|512|

> zend_optimizer.optimization_level的值是要启动的进程代码的和。

## PHP Accelerator

PHP Accelerator是一款免费的PHP加速器，可以通过简单的配置实现对PHP代码的优化。

## PHP Accelerator 配置

如果要对PHP Accelerator进行配置，可以直接编辑php.ini文件并增加相应的参数。

### PHP Accelerator的启动与关闭

启动与关闭PHP Accelerator可以通过php.ini文件中增加phpa参数来实现

```ini
phpa = on
```

默认情况下PHP Accelerator是启动的，如果需要关闭PHP Accelerator，只需要将phpa参数设置成off即可

### 文件缓存目录的设置

PHP Accelerator需要使用文件缓存目录来存放其进行代码时的临时文件，其默认值为`/tmp`

```ini
phpa.cache_dir = /tmp
```

### 修改PHP Accelerator使用的共享内存的大小

PHP Accelerator还需要使用共享，其大小默放值为8MB

```ini
phpa.shm_size = 8
```
