# Special Folder Names
大多数情况下，你可以选择你自己喜欢的名字来命名组织工程目录。但是Unity保留了一些目录名用来做特殊处理。比如编辑器脚本应该放在Editor目录下来保证正确运行。完整的Unity保留目录列在下面。

## Assets
Assets目录是Unity工程存放资源的主要目录。Project view 直接对应Assets 目录。很多API函数都假设所有的都在Assets目录下，而不需要显式的提及。可是有些函数确实需要Assets目录包含在路径中（比如AssetDatabase）

## Editor
所有在Editor下（包括子目录）的脚本都被当作是编辑器脚本，而不是游戏运行脚本。这些文件用来在开发的时候给编辑器添加功能，而不是不能在开发结束游戏运行时被用到。一次可以有多个Editor目录被使用，但是注意但是编辑器目录的位置影响了其它脚本的编译。查看 Special Folders and Script Compilation Order。注意如果脚本在Editor目录下，Unity将会不允许脚本从MonoBehaviour继承而作为组件挂在GameObject上。

## Editor Default Resources
编辑器脚本可以使用EditorGUIUtility.Load函数在需要时使用资源。这个函数检查在Assets目录下的Editor Default Resources目录。

## Gizmos
Unity的Gizmos允许你在场景中添加图形来帮助你可视化设计。Gizmos.DrawIcon函数在场景中放置一个icon来标记一个特殊的位置。这个icon需要被放在一个叫Gizoms的目录中。

## Plugins
Unity 允许你使用插件来扩展功能，插件可以是用C/C++编写的DLL。它们可以被第三方访问，可以被系统调用以及其它Unity本身不提供的。插件必须放在Plugins目录下，这会影响脚本编译顺序。查看 Special Folders and Script Compilation Order。

## Resouces
一般而言，你可以在场景中创建实例，Unity同时也允许你从脚本中载入资源。你可以吧资源放在Resources目录下（包括子目录）。这些资源可以被Resouces.Load 函数访问。

## Standard Assets
当你从标准资源包中引入资源的时候，资源被存在Standard Asset目录中。因为包含来资源，所以这些目录也能影响脚本的编译顺序，查看Special Folders and Script Compilation Order。

## StreammingAssets
在构建游戏包的时候很多游戏资源被直接打入安装包，但是有些时候你需要从一个独立的文件中访问它的原始格式，比如，在iOS上播放一个视频。你必须从文件系统上访问这个视频而不是视频纹理。如果你把这个文件放在StreamingAssets中，这个文件将会被拷贝到目标机器中。查看Streaming Assets。TODO

## WebPlayerTemplates 
略



