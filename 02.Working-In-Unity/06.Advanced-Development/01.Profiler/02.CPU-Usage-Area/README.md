# CPU Usage Area
CPU使用图在你游戏跑起来的时候它显示。当它被选中时，底下的面板显示了被选中帧的层次时间数据。

* Hierarchy 模式：显示Hierarchy时间数据。
* Grou Hierarchy模式：按照逻辑分组（渲染，物理，脚本），因为有些脚本可以在不同的组中，所以所有组的百分比加起来大于100%。这不是个bug。

## 选中单独的项
当下半部分面板中的某一项被选中，它所对应的CPU图表会被高亮（其实是其余部分被置灰）。再次点击该项取消选中。在hierarchical 时间数据 self数据表示特定函数自身的消耗时间而不包含子函数的时间。在上图例子中，41.1%是Camera.Render函数总的。这个函数做了很多事情，调用了很多draw和cull函数。排除这些函数只有2.1%的时间是消耗雜iCamera.Render函数上的。Time ms 和 Self ms栏显示同样的信息，但是以时间为单位。所以说，Camera.Render花了0.01ms，但是把所有函数算进来，0.21ms消耗。GC Alloc 栏显示了当前帧分配了多少内存，这些内存接下来会被垃圾收集器回收。如果你的代码能保持这个值是0，那么你可以避免GC引起你的帧率“打嗝”。

在面板中的Other，记录了没有落进Render，Scripts，Physics，GG或者VSync的数据，包括：动画，AI，音频，粒子，网络，加载，玩家循环。

## 物理标记
简单介绍一下一些高层的物理Profiler

## 性能警告
这里是一些比较常见的profiler检检测出来警告你的性能问题。当查看CPU使用的时候，这些警告出现在下半面板中。
下面这些情况会被profiler检测到：
* Static Collider.Modify (Expensive delayed cost)
* Static Collider.Move (Expensive delayed cost)
* Static Collider.Create (Expensive delayed cost)
* Animation.DestroyAnimationClip [Triggers RebuildInternalState]
* Animation.AddClip [Triggers RebuildInternalState]
* Animation.RemoveClip [Triggers RebuildInternalState]
* Animation.Clone [Triggers RebuildInternalState]
* Animation.Deactivate [Triggers RebuildInternalState]
上图中，警告栏显示Static Collider.Move。警告栏显示了当前帧被触发了12次。“Delayed Cost” 表示虽然profiler显示比较小的cost，但是这将触发接下来非常大的消耗。
