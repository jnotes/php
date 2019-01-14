# Trait

看上去既像类又像接口，其实都不是，Trait可以看做类的部分实现，可以混入一个或多个现有的PHP类中，其作用有两个：表明类可以做什么；提供模块化实现。Trait是一种代码复用技术，为PHP的单继承限制提供了一套灵活的代码复用机制。

当前类中的方法会覆盖trait方法，而trait方法会覆盖基类中的方法

```PHP
trait ezcReflectionReturnInfo {
    function getReturnType() {
      // code...
    }
    function getReturnDescription() {
      // code...
    }
}
class ezcReflectionMethod extends ReflectionMethod {
    use ezcReflectionReturnInfo;
    // code...
}
class ezcReflectionFunction extends ReflectionFunction {
    use ezcReflectionReturnInfo;
    // code...
}
```
