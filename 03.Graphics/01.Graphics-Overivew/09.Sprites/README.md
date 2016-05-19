# Spretes
Sprite是2D游戏对象。如果你使用3D，那么Sprites就指的是纹理，但是合并以及管理sprite 纹理是一项技术活。

Unity 提供了Sprite Creator，内建的Sprite Editor，Sprite Renderer，Sprite Packer

查看导入和设置Sprite。

## Sprite Tools
### Sprite Creator
使用 Sprite Creator在你的项目中创建占位符，这样你就可以不用等待图形

### Sprite Editor
Sprite Editor 是你可以在大图中提取sprite，然后编辑图片。比如你可以把手，脚，身体从角色中分离。

### Sprite Renderer
sprite使用Sprite Renderder组件渲染，而不是使用3D 模型的Mesh Renderer。使用Sprite Rendderer来渲染2D或者3D场景。

### Sprite Packer
使用 Sprite Packer 来优化显存的性能。

## Importing and Setting Up Sprites
sprite 是Unity工程中的一种资源，你可以通过project 视图看到他们，使用他们

有两种使用sprite的方式
1. 直接把图片拖入Assets目录
2. Assets - Import New Asset 选中

查看Import Asset获取更多信息。

### Setting your image as a Sprite
如果你的项目模式是2D，你导入的图片自动会被设置成Sprite。
可是如果你项目设置成3D，那么导入的图片就会被设置成Textrue，所以你需要改变资源的纹理格式
1. 选中资源
2. 设置纹理的格式为Sprite
