# Rendering Statistics Window
Game 窗口有个Stats按钮。当这个按钮被按下时，一个层叠窗口显示实时渲染数据，这些对性能优化来说非常有用。确切的数据非常取决于构建的目标。

窗口包含以下信息：

Time per frame and FPS 每一帧的时间（fps的倒数）。注意这个只包括了在game view中每帧更新和渲染的时间，并不包括编辑器其它的消耗。
Batches 合批的概念指的是引擎试图去合并多个渲染数据从而来减少CPU喜爱资源切换上的额外消耗。
Saved by batching 被合并的批次。为了确保良好的合批，你应该在不同对象之间共享材质。不断改变渲染的状态会打破渲染的合并
Tris and Verts 绘制的三角形和顶点的数量
Screen 屏幕的大小，取决于抗锯齿的程度和内存的使用
SetPass 渲染的批次数量。每一次需要Unity来远行时绑定一个新的shader（这会有cpu消耗）
Visible Skinned skined mesh rendered 数量
Animations 正在播的动画的数量

也可以查看profiler 的 rendering部分，哪里提供更多更具体的统计。
