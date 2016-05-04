# Profiler window 
## Attaching to Unity players
把Profiler连接到其他设备是可以的。Active Profiler的下拉菜单展示了本地网络中所有在运行的游戏。这些运行实例通过它们的类型和host name区分。运行实例必须使用Development Build模式运行才可以连接。在Build Setting对话框中，可以选择让编辑器和运行实例在启动的时候就连接起来。

## Profiler Controls
窗口上方是Profiler Controls，使用它可以打开／关闭profiler，逐帧跑。右上方有transport按钮。注意当游戏在跑以及profiler在收集数据的时候，按下任何transport按钮都会使游戏暂停。能够控制跑到收集的第一帧，往前往后逐帧，跑到最后一帧。Profiler并不会保留所有搜集的信息，所以这里所谓的第一帧表示在内存中的最就的那个信息。current transport按钮将导致profile统计当前帧。Active Profiler允许你选择是否profiler在编辑器或者独立运行的实例中（比如iOS设备）

### Deep Profilling
当你打开Deep Prfile，所有你的脚本都会被profile，也就是说所有函数调用将会被记录。这将能准确反映你代码消耗的时间。

注意Deep Profilling 将会导致非常大的消耗以及使用非常非常多内存，这将导致你的游戏将会因此跑得很慢。如果你使用了非常复杂的脚本，Deep Profilling 设置是不能使用的。Deep profile应该对非常小的游戏非常简单的脚本使用。如果你发现Deep Profilling你整个游戏帧率下降非常明显，甚至游戏都不能再跑起来了，你应该考虑不再使用这种方式，你可以使用下面介绍的方式，你会发现Deep profile对你设计游戏以及实现关键功能非常有用。注意，大型游戏使用deep profiling可能引起Unity run out of memory 所以这也是大型游戏不能使用deep profiling的原因之一。

手动的在你脚本中写profile代码将会被Deep Profiling 方式小很多消耗。可以使用Profiler.BeginSample和Profiler.EndSample函数来profile一段代码。

### SynTime
当运行锁定帧率或者垂直同步时，Unity记录需要等待的时间。默认情况下这个时间回显示在profiler中。你可以打开View SyncTime，去查看等待了多少时间。这也是测试你每帧还有多少空间的一种方式。

## Profiler Timeline
当运行游戏的时候，每一帧的数据被记录下来，同时最近的好几百帧显示。在某一帧上点击将会在下半部分显示详细信息。当前选中的时间线区域决定了显示的信息。

垂直的尺寸被自动管理，填满整个窗口。注意为了获得更多CPU使用情况的区域，你可以把内存和渲染区域移除。同时区域之间的分割线是可以被选中调节的。

时间线包含了几个模块：CPU，渲染和内存。这些取悦可以通过点击面板上的close button来移除。可以通过Add Area按钮重新加回区域。

注意在区域面板上的颜色小方块关联相应的时间。可以通过点击它移除相关的采样。小方块将会灰色，数据将会从图表中移除。这个在指出CPU图表尖锐的时候比较有用。



