# ShaderLab:SubShader Tags
Subshaders 使用tags 来高速渲染引擎啥时候怎么渲染。

## Syntax
```
Tags {
    "TagName1" = "Valuel"
    "TagName2" = "Value2"
}
```
指定来一个值为Value1的TagName1，值为Value2的TagName2。你可以使用更多。

## Details
tags 是基本的key－value对。在子shader中的tag用来决定渲染顺序及其子shader的其它参数。注意一下tags必须在subshader块而不是在pass块中。

除了内建的tag，你还可以使用你自己的tag，然后使用Materila.GetTag。

### Rendering Order -Queue tag
你可以使用Queue tag来决定对象绘制的顺序。shader确定了对象渲染的顺序，所有透明的都会在不透明的之后。

有四种预定义的渲染队列，但是有更多队列。预定义的队列是：

* Backgroud 这种渲染队列第一个渲染。你一般用来渲染背景。
* Geometry 默认选项，这个大多数对象使用，不透明的几何物体。
* AlphaTest alphatest物理使用。
* Transparent 在Geometry和Alphatest之后。
* Overlay 
```
Shader "Transparent Queue Example" {
    SubShader {
        Tags {"Queue" = "Transparent"}
        Pass {
        }
    }
}
```
对于特殊的用户想要使用中间的渲染队列。Background 1000， Gemetry 2000， AlphaTest 2450， Transparent 3000，Overlay 4000，所以想要中间的可以这么写：
```
Tags {"Queue" = "Geometry+1"}
```
因为渲染队列是2001,这将会使得对象在所有不透明对象后渲染，但是在透明物体前。在你需要一些对象在其它对象之间渲染的时候很有用。比如，透明的水应该在其它透明对象之前以及不透明对象之后。

2500之前认为是不透明的。高的渲染队列值被认为是透明对象。天空盒在透明和不透明对象之间。

### RenderType tag
TODO

### RenderType tag
TODO

### DisableBatching tag
TODO

### ForceNoShadowCasting tag
TODO

### IgnoroProjector Tag
TODO

### CanUseSpriteAtlas Tag
TODO

### PreviewType tag
TODO

## See Also
pass 也可以用tags，参看
