# Sprite Renderer
Sprite Renderer组件使你可以可以在2D或者3D场景中使用Sprite来显示图片。

可以通过Component > Rendering > Sprite Renderer 在GO上添加组件，或者你可以之间创建一个带有Sprite Renderer组件的GO通过 GameObject > 2D Object > Sprite

|Property|Function|
|:--:|--|
|Sprite|需要被渲染的Sprite对象|
|Color|渲染网格顶点颜色|
|Flip|在X或者Y上翻转|
|Material|渲染所用的材质|
|Sorting Layer|渲染时所用的层叠优先级|
|Order In Layer||

## Details
在3D图形学中，一个物体的伴随着看他的视角以及灯光，位置的变化而变化。但是在2D中，图片只是简单的显示在屏幕上，并没有transform的概念，只有基本的位置，大小和旋转。一个图形的位置通过2D坐标系给出，所以没有深度的概念，也没有摄像机的距离的概念。

可是确定不同sprite的层叠优先级仍然非常重要（比如遮挡关系）。比如，在赛车类游戏中，一辆汽车开过一块平地。Unity使用来sorting layers的概念允许你给sprite分组。sorting layer低的将被高的遮挡。

有时候需要处理同一sorting layer的层叠关系。order in layer属性可以用来确定在同一个layer中的sprite优先级。和sorting layer一样，低的会被高的覆盖。

## Rendering
一个sprite渲染使用来sprite中提供的纹理，同时使用材质上的其它熟悉以及shader。这意味着你可以使用同一个材质来渲染不同的sprite，并不用担心材质上使用哪个纹理。

sprite 渲染在材质上，使用位置，颜色，每个顶点的UV（没有法线）。如果你的材质需要法线向量，你需要使用vertex shader来计算。

sprite 默认的shaders有两个：
* sprites/default 简单的alpha 混合shader，并不处理场景中的灯光
* sprites/diffuse 简单的alpha 混合shader表面shader，并不处理灯光。这个会产生前面向量。

## Flipping
sprite可以通过设置transform.scale 为负数来翻转，这会导致GO也翻转，以及碰撞体翻转，可能会带来一些不便。

SpriteRenderere翻转的属性提供了一个轻量级翻转，并不会影响其它组件和GO。这之后简单的翻转渲染sprite，其它啥都不做。
