# ShaderLab:UsePass
UsePass 命令使用在其它shader中的命名pass

## Syntax
```
UsePass "Shader/Name"
```
插入来自指定shader的所有pass，避免代码的冗余。比如，你在某个shader中画了一个对象的轮廓，然后你想要重用这部分。UsePass命令就是包含了从其它shader来的pass。一个例子：使用一个pass，赖在内建VertexLit shader中SHADOWCASTER。

为了使用UsePass，pass必须命名。

注意，所有pass的命名都是大写，所有UsePass引用大写。
