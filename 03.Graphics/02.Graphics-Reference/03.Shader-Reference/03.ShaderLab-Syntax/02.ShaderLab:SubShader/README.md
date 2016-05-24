# ShaderLab:SubShader
每一个Unity里的shader都包含来一系列子shader。当Unity想要显示一个网格的时候，它将会找一个shader来使用，他会选择第一个能在用户显卡上跑的子shader

## Syntax
```
Subshader {
    [Tags]
    [CommonState]
    Passdef
    [Passdef ... ]
}
```
定义了tag，common state 和一系列pass

## Details
一个子shader定义了一系列渲染pass，以及一些pass常用的设置。tags是一个子shader额外可以设置的。

当Unity选择了某个子shader，每个pass定义会渲染一次对象，有时候因为光照的影响会更多。因为一个pass是非常耗性能的，所有你你应该尽可能得少使用pass。当然，有些时候，在一些显卡上一次pass并不能满足需求，这时候你就必须使用多次pass。

pass可以是 regular pass， use pass， grab pass

任何允许在pass定义出现的语句都可以出现在子shader的块中。这将会使所有pass共享这个state。

## Example
```
Subshader {
    Pass {
        Lighting Off
        SetTextrue [_MainTex] {}
    }
}
```
该子shader定义了一个pass，关掉了灯光，仅仅是用_MainTex显示mesh
