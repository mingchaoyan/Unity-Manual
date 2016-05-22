# ShaderLab:Properties
着色器可以定义一系列在Unity材质inspector上列出来给美术设置的参数。shader原文件中的属性块在此页面描述。

## Sysntax
### Properties
```
Properties {
    Property 
    [Property ...]
}
```
在属性块可以在花括号之间定义好多属性。

### Numbers and Sliders
```
name ("display name", Range(min, max)) = number
name ("display name", Float) = number
name ("display name", Int) = number
```
以上定义了很多有默认值的属性。Range类型将会在min和max之间产生一个silder。

### Colors and Vectors
```
name ("display name", Color) = (number, number, number, number)
name ("display name", Vector ) = (number, number, number, number)
```
定一个有默认值的颜色属性，有RGAB分量，或者一个4D分量。颜色属性有一个颜色拾取器。

### Textures
```
name ("display name", 2D) = "defaulttexture" {}
name ("display name", Cube) = "defaulttexture" {}
name ("display name", 2D) = "defaulttexture" {}
```
 定义了2D 纹理，立方体map和3D属性。

## Details
shader中每个属性都对应一个名字，在Unity中，推荐属性名称使用下划线开头。在材质的监视面板中，属性将会以display name显示出来。属性的默认值被被赋值。
* Range和Float属性的默认值是一个数字，比如13.37
* Color和Vector属性的默认值是在括号中的四个数字
* 2D或者Cube，默认值是一个孔子付出，或者内建的纹理

在接下来固定管线的部分中，属性值可以被方括号中中的属性名所访问到。比如你可以把两种材质属性混合，使用Blend命令：Blend[_ScrBlend] [_DesBlend]

着色器的参数会被序列化为材质数据。Shader其实可以有更多类似矩形，向量和浮点数的参数，可以在运行时设置材质。但是如果这些值并不是属性的一部分，那么他们不会被保存。在完全代码驱动的时候非常有用。

## Property attributes and drawers
在属性之前，attibutes可以被指定。这些要么是Unity的attribute，要么是你自己定义的来控制如何渲染的。Unity中的Attribute
* [HideInInspector] 不要在材质的inspector面板中显示
* [NoScaleOffeset] 纹理属性将没有tiling/offset字段
* [Normal] 纹理属性带一个法向量
* [HDR] 纹理属性带HDR
* [PerRendererData] 纹理属性带一个per-renderer数据

## Example
```
// properties for a water shader
Properties
{
    _WaveScale ("Wave scale", Range (0.02,0.15)) = 0.07 // sliders
    _ReflDistort ("Reflection distort", Range (0,1.5)) = 0.5
    _RefrDistort ("Refraction distort", Range (0,1.5)) = 0.4
    _RefrColor ("Refraction color", Color) = (.34, .85, .92, 1) // color
    _ReflectionTex ("Environment Reflection", 2D) = "" {} // textures
    _RefractionTex ("Environment Refraction", 2D) = "" {}
    _Fresnel ("Fresnel (A) ", 2D) = "" {}
    _BumpMap ("Bumpmap (RGB) ", 2D) = "" {}
}
```

