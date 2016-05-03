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
