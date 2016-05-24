# Shader Level of Detail
Shader的LOD指定了只在LOD值小于指定值的时候使用shader

默认的LOD 是无限的，也就是说只要硬件支持所有shader就会使用。但是，有时候即使硬件支持，你也可能想要舍弃一些shader细节。比如，一些低端显卡啃根支持所有功能，但是当功能跑起来的时候太慢来。所以你可能并不想要并行发现功能。

Shader LOD可以在每个shader上使用，也可以设置为全局的。

在自定义的shader上，使用LOD 命令来设置所有子shader的 LOD 值

Unity内建的LOD如下：
* 顶点光照 100
* Decal，反射 顶点光照 150
* 漫反射 200
* 细节漫反射，无光反射，顶点光照反射 250
* 高光，镜面 300
* bumped specular 400
* parallax 500
* parallax 高光 600
