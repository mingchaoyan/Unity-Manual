# ShaderLab: GrabPass
GrabPass是一个特殊的Pass，它会截取屏幕的内容。这些截取的纹理可以在接下来的pass中使用。

## Syntax
GrabPass 属于一个子shader。有两种形式:
* 仅仅GrabPass {} 将会获取当前屏幕内容作为一个纹理。纹理能够被接下来的pass使用，_GrabTexture。注意这种grab pass 将会有非常耗的抓取屏幕的操作。
* GrabPass {"TextrueName"} 只会抓取每帧的第一个物体中使用TextrueName的纹理。这个纹理可以在后续的pass中被访问。这种方式比较高效。

## Example
比较消耗性能的例子
```
Shader "GrabPassInvert"
{
    SubShader
    {
        // Draw ourselves after all opaque geometry
        Tags { "Queue" = "Transparent" }

        // Grab the screen behind the object into _GrabTexture
        GrabPass { }

        // Render the object with the texture generated above, and invert the colors
        Pass
        {
            SetTexture [_GrabTexture] { combine one-texture }
        }
    }
}
```
这个shader有两个pass，第一个pass 抓取来渲染时候的对象，然后在第二次pass中应用。当然同样的效果使用inmvert blend 模式将会更高效

## See Also
regular pass command
