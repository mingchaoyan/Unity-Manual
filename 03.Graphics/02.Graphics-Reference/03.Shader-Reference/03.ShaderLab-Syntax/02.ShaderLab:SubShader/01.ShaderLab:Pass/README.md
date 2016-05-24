# ShaderLab:Pass
一个pass块会导致一个几何对象一次渲染。

## Syntax
```
Pass {
    [Name and Tags]
    [RenderSetup]
}
```
这个基本的pass命令包含了一系列渲染状态和设置命令

## Nmae and tags
一个Pass能够定义名字以及任意多个Tags，tags是名字／值 字符串用来和渲染引擎交流

## Render State Setup
一个Pass的设置变量设置了显卡的不同状态，比如是否开启alpha blending，是否使用深度测试等等，这些命令如下：

### Cull
```
Cull Back | Front | Off
```
设置了多边形裁剪模式，查看具体页面。

### ZTest
```
ZTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always)
```
设置了深度buffer的测试模式

### ZWrite
```
ZWrite On | Off
```
设置了深度buffer的写模式

### Blend 
```
Blend SourceBlendMode DestBlendMode
Blend SourceBlendMode DestBlendMode, AlphaSourceBlendMode AlphaDestBlendMode
```
设置了alpha blend模式

### ColorMask
```
ColorMast RGB | A | 0 | any combination of R, G, B, A
```
设置了颜色通道的写入掩码。写入掩码0 关闭所有渲染通道。默认的卸乳乳模式是RGBA所有通道，但是对于某些特殊效果，你啃根需要某些通道不变或者关闭某些通道。

### Offset
```
Offset OffsetFactor, OffsetUnits
```
设置Z buffer深度

## 历史固定管线shader命令
历史的固定管线有很多命令。这些都是被废弃的功能，因为写表面shader或者顶点和片段shader会更灵活。可是有些情况下使用固定管线的shader将会非常容易。当不使用固定管线shader的时候，所以这些命令都会被忽略。

### Fixed Functions Lighting and Material
```
Lighting On | Off
Material {Material Block}
SeparateSpecular On | Off
Color Color-value
ColorMaterial AmbientAndDiffuse | Emission
```
所有这些命令控制了每个顶点的灯光开关，材质颜色，镜面高光，默认的顶点关注以及多少mesh 顶点会被灯光影响。

### Fixed Function Fog
```
Fog {
    Flog Block
}
```
设置固定管线的雾参数

### Fixed Function AlphaTest
```
AlphaTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always) CutoffValue
```
打开固定关系的alpha test

### Fixed Function Texture Combiners
等到渲染设置好了，你可以指定一系列纹理和其它模式。
```
SetTexture textureProperty { combine options }
```

## Details
Shader pass 被Unity的渲染管线影响。比如一个pass指定了只能使用derred shading。某些pass可以被同一个对象执行多次，比如如果有多个灯光forward 渲染将会渲染多次。

## See Also
有些特殊类型的pass，比如
* UsePass 包含一个其它shader的pass
* GrabPass 能够截取当前屏幕的内容，然后在接下来的pass中使用
