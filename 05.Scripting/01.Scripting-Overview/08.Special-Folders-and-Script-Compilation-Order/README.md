# Special Folders and Script Compilation Order
大多数情况下，你可以自己创建喜欢的目录名，但是Unity保留来某些目录用做特殊目的。有些目录对脚本的编译有一定影响。有4个基本的脚本编译阶段而且脚本编译的阶段取决于他的父目录。

脚本会引用其它脚本的类。一条基本的规则就是——*在后一个阶段编译的脚本不能在本脚本被引用，在前编译阶段的脚本可以被本脚本引用*

另一条原则，需要引用不同语言的类必须在前编译阶段被编译。

以下是4个编译阶段：
1. Standard Assets, Pro Standard Assets 和 Plugins下面的脚本
2. Standar Assets/Editor, Pro Standard Assets/Editor 和 Plugins/Editor 下的脚本
3. 所有其它不在Editor下的脚本
4. 剩余的脚本
