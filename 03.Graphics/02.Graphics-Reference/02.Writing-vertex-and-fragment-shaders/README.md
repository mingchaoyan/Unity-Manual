# Writing vertex and fragment shaders
shaderlab 着色器包含多余硬件着色器。他们可以做很多事情。描述材质inspector中的属性，包含不同硬件上实现的子shader，设置固定管线状态等等。真正可编程shader——就像顶点和片段程序－只是shaderlab的一部分。参看shader手册。这里我们统一称这种低等级的硬件shader为shader程序。

如果你的shader有光照影响，请参看表面shader文档。本部分假设所有shader都不受Unity光照影响。

shader程序用Cg/HLSL语言编写，在shader源文件中作为片段存在。比如某些地方Pass通道命令，他们看起来是这样子的：
```
  Pass {
      // ... the usual pass state setup ...
      
      CGPROGRAM
      // compilation directives for this snippet, e.g.:
      #pragma vertex vert
      #pragma fragment frag
      
      // the Cg/HLSL code itself
      
      ENDCG
      // ... the rest of pass setup ...
  }
```

## Cg/HLSL snippets
Cg/HLSL程序片段写在CGPROGRAM和ENDCG之间。

在程序片段开始的地方可以使用#pragma 语句，来指定哪些shader函数的编译：
* #pragma vertex name 编译名叫name的顶点shader
* #pragma fragment name 编译名叫name的片段shader
* #pragma geometry name 编译名叫name的DX11 hull shader。这个选项在 #pragma target 5.0 开启的时候自动开启。
* #pragma domian name 编译名叫namde 的DX11 domain shader。这个选项在 #pragma target 5.0 开启的时候自动开启。
其它编译命令
* #pragma target name shader编译目标，看下
* #pragma exclude_renderers space separated names 只对给定的渲染使用shader,默认shader对所有渲染有效。
* #pragma multi_compile 多shader变量
* #pragma enable_d3d11_debug_symbols 生成DX11的调试信息，可以在vs12（或者更高版本）中调试
每个片段至少包含一个顶点程序和一个片段程序。所以#pragma vertex 和 #pragma fragment 命令是必须的。

在Unity 5.0中没用的编译命令可以被安全的移除。比如#pragma glsl, #pragma glsl_no_auto_normalization, #pragma profileoption, #pragma fragmentoption

## Shader targets
默认的，unity编译shader2.0。可以使用#pragma target 来允许shader被编译成其它兼容等级。以下是支持的shader模型，兼容级别逐渐提高(需要更高的GPU性能)。

### pragma target 2.0(default)
* Unity支持的所有平台。DX9 shader 模型2.0
* 有限的算术和纹理命令，8个解释器，没有顶点纹理采样。没有片段shader命令，没有显式的LOD纹理采样。
TODO

## Rendering platforms
Unity支持很多渲染API（比如Direct3D 和 OpenGL），默认情况下所有shader程序会被编译支持所有的渲染。你可以使用#pragma exclued_renderers 命令和 #pragma only_renderers 指定渲染器。在你想要显式的使用某些shader语言特性，但是你并不知道其它平台的情况下比较有用，当前支持的渲染器名字有：
* d3d9 - Direct3D 9.
* d3d11 - Direct3D 11/12.
* opengl - OpenGL 2.1.
* glcore - OpenGL 3.x/4.x.
* gles - OpenGL ES 2.0.
* gles3 - OpenGL ES 3.x.
* metal - iOS/Mac Metal.
* d3d11_9x - Direct3D 11 9.x feature level, as commonly used on WSA/WP8 platforms.
* xbox360 - Xbox 360.
* xboxone - Xbox One.
* ps3 - PlayStation 3.
* ps4 - PlayStation 4.
* psp2 - PlayStation Vita.
* n3ds - Nintendo 3DS.
* wiiu - Nintendo Wii U.
* 比如，下面这句将会只编译shader进D3D9模式
```
#pragma only_renderers d3d9
```

## See Also
