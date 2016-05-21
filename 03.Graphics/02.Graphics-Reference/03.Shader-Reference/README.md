# Shader Reference

在Unity中Shader 可以使用三种方式
* 表面shader
* 顶点和帧shader
* 固定函数shader

shader tutorial 可以给你一个你需要的选择。

无论你使用哪一种shader，shader 代码使用一种叫做ShaderLab的语言来组织shader结构
```
Shader "MyShader" {
    Properties {
        _MyTexture ("My Texture", 2D) = "white" { }
        // other properties like colors or vectors go here as well
    }
    SubShader {
        // here goes the 'meat' of your
        // - surface shader or
        // - vertex and program shader or
        // - fixed function shader
    }
    SubShader {
        // here goes a simpler version of the SubShader
        // above than can run on older graphics cards
    }
}
```
我们建议你从熟悉ShaderLab语法开始，然后转向表面shader或者顶点帧shader。应为固定函数shader只能用ShaderLab编写，你会在ShaderLab手册中看到他。

以下手册包含来很多不同类型的shader，尤其是表面shader，你可以从Unity官网获得Unity内建的shader，Unity的Image Effect 包也包含来很多有趣的顶点和帧shader。

先去看shader tutorial吧！
