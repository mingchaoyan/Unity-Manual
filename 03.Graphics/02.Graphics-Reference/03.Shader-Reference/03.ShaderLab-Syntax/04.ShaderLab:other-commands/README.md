# ShaderLab:other commands

## Category
category 是一个以下命令的逻辑分组。在继承rendering状态很有用。比如，你的shader可以有多个子shader，每个需要雾效果关，混合效果开等等。你可以这么使用
```
Shader "example" {
    Category {
        Fog { Mode Off }
        Blend One One
        SubShader {
            // ...
        }
        SubShader {
            // ...
        }
        // ...
    }
}
```
category块只会影响着色器的解析，它的效果和粘贴到每个子shader的效果是一样的。而且他并不能对shader的执行速度有影响。
