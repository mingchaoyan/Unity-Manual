# Scripting Restrictions
Unity 努力提供跨平台的API和体验。可是有些平台有内在的限制。下表展示了所有平台的限制：
除了Android －Mono 和 Standalone－Mono 其它都至少限制要AOT

## Ahead-ofptime compile
一些平台并不允许运行时生成代码。所以晕倒JIT的代码在目标设备上就会fail。我们需要AOT方式编译所有托管代码。这两种编译方式的差别并不是主要的，主要的是有些API，在AOT平台上使用的时候需要额外的注意

### System.Reflection.Emit
AOT平台不能实现System.Reflection.Emit命名空间下的任何方法。注意System.Reflection下的其它方法是可以用的，只要编译器可以推断出需要反射的代码是存在的。

### Serialization
AOT平台将会因为使用反射遇到序列化的问题。如果类型或者方法只是通过反射的方式作为序列化或者反序列化使用，那么AOT编译器不能检测到代码。

### Generic virtual methods
范型方法需要编译器在实际运行在设备上时对开发时写的代码做额外的工作来扩展。比如我们去要List的不同版本int和double。
TODO

## No threads
有些平台并不支持使用线程，所以使用System.Threading 命名空间下的托管代码将会fail。同时一些.NET类库隐式地依赖线程，比如经常使用的System.Timers.Timer类。
