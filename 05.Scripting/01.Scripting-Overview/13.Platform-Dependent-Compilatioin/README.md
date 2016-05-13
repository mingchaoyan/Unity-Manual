# Platfrom Dependent Compilation
Unity 有平台依赖编译的功能。通过一些预处理指令让你可以把代码按照平台分成几部分，然后分开编译和执行。

而且你可以在编辑器中执行这些代码，所以你可以为移动平台或者控制台编译代码但是可以在编辑器中测试它们。

## 宏
一系列宏
...

同时你可以依赖你的版本
一系列宏

注意：2.6版本之前没有宏可以定义，因为这个功能是在那个版本引入的

你可以使用DEVELOPMENT_BUILD定义是否你的脚本需要打开Development Build模式

## 测试预编译代码
下面展示一个怎样使用预编译代码的小例子。这些例子根据你选择的平台打印消息。

首先选择一个你想要测试代码的平台，通过File->Build Settings，选好以后点击switch。然后当你运行的时候根据你选择的平台，某一条信息会答应在Unity Console中。

除了#if #endif ，你还可以用多路测试 #if #elif #else #endif

## 平台自定义宏
Player Setting 面板中的Other Setting模块
冒号隔开

## 全局自定义宏
你可以定义你自己的预处理命令来控制需要编译进的代码。你需要添加一个包含预定义命令的文本文件在Assets/目录下。文件的名字取决于你所用的语言，后缀名统一为.rsp.
* C# smcs.rsp
* C# Editor gmcs.rsp
* UnityScript us.rsp
比如，你可以包含单独一行"-define:UNITY_DEBUG"在smcs.rsp文件中，于是UNITY_DEBUG宏将会全局存在C#代码中，但是不包括编辑器代码。

每次你改动了rsp文件你需要重新编译才能生效。你可以故意该动或者重新导入js或者cs文件来达到重编的目的。

如果你仅仅需要改变全局宏，你可以使用Player Setting中的符号，哪里会覆盖到所有编译器。如果你选择了使用rsp文件，你必须给每一个Unity使用到的编译器都提供一个rsp文件，你不知道哪个在使用哪个没有使用。

rsp文件的使用在smcs应用的help文档中有描述。你可以运行smcs -help 获得更多的信息。同时记着，rsp文件需要匹配被调用的编译器。比如，编译目标是web player，smcs使用smcs.rsp；当目标是标准平台用户，gmcs使用gmcs.rsp；当目标是微软编译器，csc使用csc.rsp
