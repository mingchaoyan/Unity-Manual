# Plgins

在Unity中，你使用脚本来创建函数，但是你依然可以包含Unity外的代码，通过使用插件。有两种插件你可以使用：托管插件和原生插件。

托管插件是被VS或者MonoD创建的.NET程序集。他们只包含.NET代码，意味着不能访问.NET不支持的库。可是托管代码也是标准.NET工具。托管插件代码和Unity脚本代码中几乎相同的使用，只是插件是在Unity外部编译，所以源代码可能不能获得。

原生插件是平台的原生库。他们拥有操作系统的系统调用，第三方库这些Unity不能提供的功能。可是这些库并不能被Unity工具使用托管的方式访问。比如说：如果你忘记添加托管的插件文件到工程下面，你将会得到标准的编译错误，但是如果你忘了原生插件，你只能在运行的时候看到报错。

本部分描述了如何在Unity工程中创建一个插件和使用插件。