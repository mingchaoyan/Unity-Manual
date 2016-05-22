# ShaderLab Syntax
Unity中所有shader文件被一种叫做shaderlab的语言编写。在源文件中，嵌套的雨呀结构描述了这个shader。比如哪些属性应该显示在材质inspector上；fallback用哪个；使用哪种混合模式；实际的shader 代码用cg 片段写在同一个shader文件中。

该页面和子页面描述了一个嵌套的shaderlab语法。cg片段使用HLSL／Cg编写，可以查看该页面。

Shader 是最根本的命令。每个文件必须定义一个且仅有一个Shader。这指示了一个对象将怎么使用这个着色器来渲染。

## Syntax
```
Shader "name" { [Properties] Subshaders [Fallback] [CustomEditor] }
```
定义了一个shader。这个shader将会在材质的inspector中以name的名字列出来。着色器的选项也可以定义在properties然后在材质的inspector中出现。这之后SubShaders，然后有一个可选的fallback和一个自定义的编辑器

## Details
### Properties
着色器有很多属性。任何在着色器上声明的属性会出现在材质的inspector。典型的属性有：对象的颜色，纹理，以及其它值。

### SubShaders & Fallback
每个着色器都有一些列sub-shaders。你必须至少有一个。当载入一个着色器的时候，Unity将会遍历subshader，然后挑选其中第一个能被支持的。如果没有能被支持的，那么就使用fallback的。

不同的显卡有不同的能力。有一个游戏开发者永恒的话题，你想要游戏在最新的硬件上渲染最好，但是不要只让这个游戏只有3%的玩家能玩。这就是subshaders的来历。创建一个你梦想中的最好的效果，然后为老显卡添加更多subshader。这些subshader可能用比较慢的方式实现了你想要的效果，或者可能选择不去实现某些细节。

### Examples
这里有一个简单的shader例子

这个shader定一个一个颜色属性，默认值为(1, 0.5, 0.5, 1)。然后一个但一个subshader包含了一个Pass使用固定管线灯光来设置基本材质。
