# Graphics Settings
这里的设置大多数用来跨项目自定义或者优化图像相关的设置。

## Built-in shader settings
这些设置允许指定在deferred shading 和 legacy deferred lighting 光照pass的时候使用的shader。

默认的值是使用内置Unity 功能，但是你可以提供你自己兼容的shader，如果你想深度定制延迟渲染。

你可以指定"No Support"如果你知道你并没有使用延迟着色或者光照，这样可以在构建游戏数据的时候节省一些空间。

## Always Included Shaders
指定一个shader列表，总是会存储在项目工程中，即使你场景中没有使用他们。流式的场景 assetbundle中的shader需要被加到这个地方来，保证他们能够被访问。

## Shader Stripping
默认情况，Unity通过检测你的场景和灯光设置来确定哪些雾效和灯光模式，然后跳过相应的shader变量。这样节省来游戏构建数据的size以及减少加载时间。
可是，如果你使用Assetbundle或者在运行时从脚本改变雾模式，你可能需要手动指定模式。

## Shader Preloading
指定一系列shader用来预加载。
