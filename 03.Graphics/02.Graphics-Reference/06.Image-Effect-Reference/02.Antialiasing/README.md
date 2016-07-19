# Antialiasing
抗锯齿是一种设计用来平滑图像的后期效果。当两块不同颜色的区域拼成一张图时，边界的像素会变得非常清晰明确。这种效果就是锯齿，同时抗锯齿也就指的是任何减小这种效果的方法。

抗锯齿算法是基于图像，当传统的多重采样不被支持的时候（比如当使用了延迟着色或者高动态渲染）就会显得非常有用。

NVIDIA支持的算法有 FXAA, FXAA II, FXAA III(这些是可修改并且终端优化的)，简单边缘模糊(NFAA, SSAA)和DLAA适应算法。SSAA是最快的算法，接下去是NFAA,FXAAII, DLAA 和 其他FXAA。当然了抗锯齿的质量和算法的速度是相反的，但是可能会有一种情况就是算法的选择并没有带来改变。

优化后的FXAA III 实现提供了一个在效果和性能之间比较合理的平衡。

其他的图像效果，你必须安装 Standard Assets Effects package

## Properties

## Hardware Support
这些效果需要显卡支持Shader 模型3
