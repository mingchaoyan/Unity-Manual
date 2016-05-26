# Optimizations
就像PC一样，像iOS和安卓这样的移动平台会有很多不同等级的性能。你可以非常容易的找到一个10倍强渲染性能的比其它手机。需要考虑的一些途径：
1. 保证基准配置上能够允许ok
2. 使用更多“视觉糖”或者高性能配置
* 分辨率
* 后期
* 多重采样抗锯齿
* 各向异性
* 着色器
* 特效／粒子密度的开关

## Foucus on GPUs
图形性能受填充率，像素和几何复杂度 (顶点数量) 的束缚。所有这些可以通过找到一些方法裁剪来达到减少的目的。因为Unity会自动剔除在视口外面的对象，所谓遮挡剔除。

在移动平台，你最基本的束缚是填充率（填充率 = 屏幕像素＊shader复杂度＊过度绘制）,过于复杂的shader常常是引起这个问题最常见的原因。所以使用Unity提供的mobile shader，或者把他们写得越简单越好。尽可能把像素着色（片段着色）移到顶点着色。

如果在质量面板中降低纹理的质量可以是游戏跑得更快，你很可能受限于内存带宽了。所以你可以压缩纹理，使用mipmap，降低纹理的大小。

LOD可以简单的随着物体的离远而消除细节。

### Good practice
移动GPU受限于他们产生的热量，他们使用的能耗，以及噪音。所以相比桌面版本，移动GPU有较低的带宽，比较低的运算性能和纹理处理能力。GPU的架构也被调到尽可能小的带宽和能耗。

Unity 已经为OpenGL ES 2.0优化过，他使用GLSL ES(和HLSL类似) 着色器语言。内建的shader一般使用HLSL（或者CG）。你也可以直接写GLSL如果你想要，但是这么做对你OpenGL平台会有限制（比如移动平台或者mac平台），因为目前为止还没有GLSL到HLSL的转换工具。当你你使用HLSL 的float/half/fixed 类型，他们会最终转为hightp mediump lowp 精度。

这里是一个最佳实践的checklist
1. 保持越少材质球。可可以使得Unity来更好的合批
2. 使用图集而不是单独的小图。这样会加载更快，状态切换也更少，更有利于合批。
3. 使用Renderer.sharedMaterial 而不是Renderer.material 如果使用图集
4. Forward 渲染像素光照是昂贵的
* 尽可能使用light maping 而不是 实时光
* 在画质设置界面调整像素光照数量。每个像素应该只有一个方向光。具体看具体情况。
5. 尝试不同的灯光渲染模式来获得合适的优先级
6. 如非必须，避免使用alpha test
7. 保持透明覆盖最小
8. 避免一个对象的多灯光模拟
9. 尽可能减少shader pass的数量
10. 渲染次序是非常关键的。一般情况下：
* 完全不透明物体
* alpht test 物体
* 天空盒子
* alpha blend 物体
11. 在移动平台后期处理是昂贵的，谨慎处理
12. 减少过度绘制，使用尽可能简单的shader
13. 每帧两次buffer

### Shader 优化
有一种很简单的方法来测试是否被填充率限制：当你降低分辨率的时候游戏是否允许得非常快。如果答案是的，那么目前限制你的是填充率

可以使用如下方法减少shader复杂度：
* 尽可能避免alpha  test，使用alpha blend版本
* 使用简单的被优化过的shader（比如Unity自带的Mobile shader）
* 避免在shader中使用昂贵的函数，比如平方，指数，log，cos，sin，tan
* 尽可能使用最少的精度格式。

## Focus on CPUs
游戏经常被GPU处理像素所限制。所以导致并没有使用完CPU的性能。尤其是多核CPU上。所以从GPU的工作中脱身然后投入到CPU优化工作中：mesh skinning，对象的合批，粒子几何体的更新。

这些应该小心使用。比如你还没有河过draw call，那么合批可能会导致更差的性能，因为她会导致遮挡剔除更加低效以及光照的影响也更大。

### Good practice
* FindObjectsOfType（以及Unity属性get访问器）是非常慢的。所以慎用
* 对于不移动的物体设置静态属性，允许Unity内部优化
* 花比较多的cpu周期来遮挡剔除，获得更好的排序

### Physics
物理是非常消耗CPU的。可以通过编辑器Profiler看到。如果表现的物理非常耗时间，可能是下列原因：
* 微调Time.fixedDeltaTime，高一点。如果游戏移动缓慢，你可能需要少一点的fixed update。这样fixedDeltaTime将会很低或者碰撞会失败
* Physics.solverIterationCount
* 使用较少的Cloth
* 只在必要处使用刚体
* 使用原生碰撞体而不是网格碰撞体
* 不用移动一个静态的碰撞体，因为它会引起巨大的性能消耗。可能在profiler中显示的是Static Collider.Move 但是实际上 Physics.Simulate被调用。如果可能，把刚体的运动学设置为true
* 在Windows平台，你可以使用NVidia的 AgPerfMon 调优同居来获得更多信息

## Android

### GPU
有很多流行的移动架构。和PC平台的厂商不一样的是有很多GPU架构。

* ImgTec PoverVR SGX
* NVIDIA Tegra 
* Qualcom 
* ARM

花点时间看看不同的渲染途径。在排序的地方花大量时间。设置一个低端机，然后在低端机上面使用profiler测试你的游戏

使用平台特定的纹理压缩格式

### Further reading

### Screen resolution

### Android version

## iOS

### GPU
只有PowerVR架构
* ImgTec PoerverVR SGX. Tile base, deffered :在瓦片格式中渲染所有物体，只有可见元素着色
这意味着
* Mipmaps 是不必要的。
* 抗锯齿和异向足够便宜，而且在iPad 3的某些情况下并不需要
TODO

### Further reading

### Screen resolution

### iOS version

## Dynamic Objects
### Asset Bundles
* Asset Bundls 在设备上缓存。
* 使用编辑器API可以创建
* 使用WWW API加载，WWW.LoadFromCacheOrDownload 或者作为资源 AssetBundles.CreateFromMemory或者 AssetBundle.CreateFromFile
* 使用AssetBundle.Unload 卸载。可以选择保留已经加载的然后卸载。所以记着当你不需要的asset需要去引用。public 和 static的变量是不会被gc的
* Resouces.UnloadAsset 卸载在内存中的特殊资源。可以在必要的时候从硬盘加载
iOS上可以同时下载多个ab吗？
下载是通过操作系统提供的异步API，所以由操作系统决定下载线程的数量。当启动多线程的时候，你需要时刻注意设备的带宽以及当前的空闲内存。每个下载需要分配一个临时buffer，所以你需要非常小心，以免内存用尽。

### Resources
* 需要被放入打包的资源 
* 给任何原始二进制文件使用.bytes扩展名
* 如果要使Unity识别为文本资源，使用.txt后缀
* 资源在打包的时候转化成平台格式
* Resource.Load()

## Silly issues checklist
* 纹理没有合理的压缩
* 不同情况不同分辨率，但是确保压缩了纹理除非你非常确定不需要。
* ETC/RGBA16 安卓的默认格式，但是会随着GPU厂商有变化。最好的途径是尽可能使用ETC。Alpha纹理可以使用两张ETC（其中一张有alpha通道）
* PVRTC iOS默认格式，各种情况都比较适用
* 使用了get/set pixels的纹理有双倍的footprint，除非确实需要，否则不勾选
* 运行时从jpeg／png载入的纹理将不会被压缩
* 大mp3文件在载入时不压缩
* 添加场景载入
* 无用的资源仍然驻留内存
* 如果随机的crash，请试着增加到2GB内存
有些时候，控制台啥也没有打印信息，只是随机crash
* 快速的脚本调用或者剥离可能导致随机的crash，在iOS尽量避免这些。
