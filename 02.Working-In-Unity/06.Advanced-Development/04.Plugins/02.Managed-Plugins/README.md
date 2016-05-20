# Managed Plugins

经常的脚本在项目中以源文件的形式存在，然后被编译进Unity。可以使用外部工具编译DLL。然后DLL可以被加进项目，它包含的类可以像普通的类那样被使用。

一般来说使用脚本比使用DLL要简单一点。可是你可以通过这种方式来用第三方库。当开发的时候，你可以使用Unity不支持的脚本（比如F# ），只需要把它们编入DLL然后添加到你的工程中。另一种情况就是你想要对外提供一个没有源代码的Unity插件(比如Asset Store)，这时候DLL是一种简单的方式。

## Creating a DLL

你首先需要一个合适的编译器来构建一个DLL。并不是所有的编译器产生的.NET代码能够在Unity中使用，所以在大量工作进行前，使用小量的测试是需要的。如果这个DLL并不包含Unity的API，那么你可以简单的把它编译成DLL。如果你使用了Unity的API你需要让编译器能够找到Unity自己的DLL。Mac上，他们在Application包里面，Unity DLL的路径一般在：
```
/Applications/Unity/Unity.app/Contents/Frameworks/Managed/
```

编译DLL的其它选项参数根据编译器的不同。比如一个比较常见的Mono C#编译器,mcs,在Mac上的命令可以是这样的：
```
mcs -r:/Applications/Unity/Unity.app/Contents/Frameworks/Managed/UnityEngine.dll -target:library ClassesForDLL.cs 
```
这里-r 选项指定了需要包含的库的路径，在这个案例中就是UnityEngine.dll。-target选项指定了那种类型的，library表示选择DLL构建。最后需要编译的源文件是ClassesForDLL.cs。加入运行OK，DLL文件的将在源文件的同一个目录下产生。

## Using the DLL
当编译好了以后，DLL文件就能像普通资源那样被拖入Unity工程。DLL资源有右上角有一个折角的可以查看里面的类。由MonoBehaviour继承的类可以托到GO上，没有从MonoBehaviour继承的类可以在其它脚本上直接使用。

## Step by Step Guide for MonoDevelop and Visual Studio
本部分表述了如何在MonoD和VS中构建和集成DLL，以及DLL的调试。

### Setting Up the Project
首先，MD或者VS中创建一个新项目。
其次，添加UnityDLL。

### Code
重命名类为MyUtilityes。在Debug 符号下编译生成DLL

### Using the DLL in Unity
创建一个新的Unity项目，DLLTest.dll拖进Assets目录。

### Setting Up a Debugging Session for the DLL

首先需要保证DLL是debug符号的。在MD中，复制dll.mdb文件进Assets/Plugins目录。VS中运行
```
Program Files\Unity\Editor\Data\Mono\lib\mono\2.0\pdb2mdb.exe
```
生车功能i 个mdb，然后复制进Assets/Plugins

接下来，打开Test脚本，确保Unity debugger插件是装上的。

这些步骤好了以后，你可以想平常那样调试了。
