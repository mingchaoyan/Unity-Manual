#Using Particle System in Unity
Unity 把粒子系统实现成了一个组件，所以在场景中添加一个例子系统就是简单的添加一个预设的object，或者在已有的object上添加一个组件。因为这个组件比较复杂，所以在inspector中被分了好几个模块，每个模块包含一堆相关的特性。而且你可以同时编辑一个或者多个系统。很多粒子系统组件的选项在组件文档中有详细说明。

当一个例子系统被选中，scene窗口中将会包含一个小的粒子系统面板，对于需要做些可视化的变动比较有用。

Playback Speed 将会允许你加速或者减速粒子系统以便你快速查看。PlaybackTime 显示了从系统开始以及流逝的时间，这个时间会被Playback Speed影响。Particle Count表示当前系统中有多少个粒子。playback time可以被鼠标拖动，面板可以暂停或者恢复粒子系统。

## Varying Properties Over Time
在运行过程中很多粒子特性甚至是整个粒子系统是可以变化的。Unity提供了不少方法改变:
* 常量：属性的值在生命过程中可以赋值；
* 曲线：指定曲线变化图
* 在两个值之间随机
* 在两个曲线之间随机

对于颜色属性，比如说Color over lifetime，有两个选项：
* 斜率
* 在两个斜率之间随机

