# Optimizing Shader Load Time
Shader 是一段跑在GPU上的小程序，在加载它需要一定的时间。单个GPU程序通常不会花费太多的加载时间，但是大量shader经常会有内部变体。
比如说，Standard shader，如果被全部编译，将会导致几千个小GPU程序，这会带来两个潜在的问题：
* 大量shader变体将会增加游戏构建时间，和游戏包大体积。
* 运行时大量shader变体会比较慢且花费比较多的内存。

## Shader build time scripping
当构建游戏的时候，Unity可以发现没有被游戏使用的内部shader，然后从构建数据中跳过他们。构建时剥离:
* 单独的shader功能，使用#pragma shader_feature.如果没有一个材质使用了一个特殊的变体，那么这将不会被构建。查看internal shader variants 文档。
* 处理雾效和Lightmapping模式的shader，如果没有场景使用，那么将不会被构建进游戏。查看Graphics Setting

两者混合将会显著降低shader的体积。比如一个完整的Standard shader将会保护上百M，但是在典型的项目中，这经常只会使用几M（而且在构建的时候经常会进一步压缩）

## Default Unity Shader loading behavior
在默认设置下，Unity会架子啊shaderlab Shader对象进内存，但是要到真正去要的时候才会去创建内部shader变体。
这就意味着被构建进游戏的shader变体依然有被使用的可能性，直到真正使用之前，没有内存和加载时间的消耗。比如shader经常会包含一个变体来处理点光源的阴影，但是如果你在游戏中没有使用点光源阴影，那么在这个特殊的变体中就没有你点光源。

默认行为的一个负面影响就是，当一个shader变体在第一次需要使用的时候，可能会有卡顿，因为新的GPU代码需要被加载到显卡中。在游戏开发中这样的体验并不好，所以Unity有一个ShaderVariantCollection 资源来帮助解决这个问题。

## Shader Variant Collections
ShaderVariantCollection 是一个Shader列表，对每个shader，会有一个Pass 类型列表和shader关键字。

创建这些资源基于真实使用的shader和它们的变体，在编辑器中能够跟踪shader和它们的变体。在Graphics Settings中又一个按钮来创建ShaderVariantCollection，或者清空当前跟踪的shader列表。

一旦你有了一些ShaderVariantCollection资源，你可以设置这些变量自动预加载，或者你可以从脚本中从shader variant collection加载。查看ShaderVariantCollection类。
