# Sprite Editor

有时候一个sprite纹理只包含一个图形元素，但是这把相关的图形集合在一张图片中是非常方便的。比如，一张图片可以包含一个单一角色，一辆汽车车身和轮子可以分开。Unity可以很方便的从合成的图片中提取元素，这都通过Sprite Editor。

注意：确保你需要的编辑的图形元素是Sprite纹理格式的。了解Sprite的基本信息请看此页面。

很多元素的Sprite纹理须需要设置成Multiple Sprite模式。

## Opening the Sprite Editor
打开Sprite Editor
1. 选中一张2D图片；
2. 点击在Texture Import Inspector中的Sprite Editor按钮

注意：只有在纹理格式设置成 Sprite的时候，你才可以看到Sprite Editor按钮
注意：Sprite Mode需要设置为Multiple，如果你的图片有很多元素。

你会看到很多控制条。右上的slider用来聚焦，颜色按钮选择你需要通过原来的样子还是alpha层次看。最右边的控制纹理的像素化。向左拉slider将会减小分辨率。最重要的控制是在左上，这里给你一个分割元素的选项。最后Apply和Revert按钮使你可以保存和放弃你刚刚做过的修改。

## Using the Editor
最直接的使用这个编辑器的方式就是手动区分元素。如果你点击图片，你就会看到一个矩形选中区域出现。你可以拖手柄或者拉动矩形的边来调整大小。如果只有一个元素，你可以拖另一个矩形来添加元素。注意到当你有矩形选中的时候，一块面板出现在你右小角。
面板中的控制条让你选择sprite的名字，然后设置矩形的位置和大小。上下左右可以设置为像素。也有pivot可以调整。

Trim按钮将会调整矩形尺寸，使他正好在图形外围。

## Automatic Slicing 
TODO

## Polygon Resizing
TODO
