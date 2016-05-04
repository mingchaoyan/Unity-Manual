# Including scripts in AssetBundles
AB能够包含作为TextAssets的脚本，但是它们不会被执行。如果如想要在AB中宝航可以在应用中执行的代码，你需要把它们预编译成assembly，然后使用Mono的反射类（注意反射在要求使用AOT编译的平台上是不可用的，比如iOS）。你可以在任何普通的C#IDE中创建你的assembies(比如Monodevelop，VS)，或者使用文本编辑器然后使用mono/.net 编译器。

注意：从ab中加载脚本在Windows Store Apps 和 Windows Phone上不支持

