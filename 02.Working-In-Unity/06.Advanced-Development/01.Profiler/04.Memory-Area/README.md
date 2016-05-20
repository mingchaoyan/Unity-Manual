# Memory Area
监视你的游戏的内存使用有两个模式。在下面板的上部，有一个下拉菜单。

## Simple View
简单模式每帧实时显示了Unity使用了多少内存。

Unity保留了已分配的内存池，放置应用过于平凡的向OS要内存。所以面板上显示了保留了多少内存以及使用了多少内存。包括以下几点：

* Unity Unity引擎代码自身使用的内存
* Mono Mono托管堆，这些内存是可被回收的
* GfxDriver 纹理，渲染，着色器，网格大约使用的内存
* FMOD 音频资源内存
* Profiler Profiler使用的内存。这个数量可能和Task Manager 或者 Activity Monitor的数据并不一致，因为有些未跟踪到的内存。这里包括的内存是使用了驱动和可执行代码的内存。

内存统计还展示了常用的资源和object
* 纹理
* 网格
* 材质
* 动画
* 音频
* 对象数量 创建的总对象数量。如果这个数量一直在增加，说明你有对象只创建并不销毁

## Detailed View
详细模式允许你获取内存的快照。使用Take Sample按钮来抓取内存。获取这些数据通常需要一些时间。当抓取了数据，profiler将会树形结构，你可以展开来看内存使用。

这将展示每个单独资源的游戏内存占用。通常会有一个这个对象在内存中的理由。理由可能是以下：
* 代码中存在引用
* 场景对象
* 内建资源
* 标记为不保存

当在编辑器中，点击列表中的对象，将会把你引到工程或者场景视图中。

当你在编辑器中调优，所有展示的内存是编辑器中消耗的。这会比实际真机上小，因为有编辑器的消耗。使用真机连到Profiler将会获得一个比较准确的值。

System.ExecuteableAndDlls 的内存值是只读的，所以OS将会丢掉这些页面重新reload。所以这些只带来一小部分内存压力也很少导致操作系统杀死应用。而且有些页面是应用间共享的。