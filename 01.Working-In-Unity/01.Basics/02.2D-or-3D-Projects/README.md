# 2D or 3D Projects
一个3D游戏的空间包括宽，高，深度(X, Y, Z)，而2D游戏只会有宽和高(X,Y)

当你在创建项目的时候，你需要决定使用2D还是3D模式。模式将决定Unity编辑器的很多设置。这些设置被列在下面。

在开发过程中，你可以不顾一开始设置的模式，在2D和3D模式中切换。有些项目既使用2D的元素，又使用3D的元素，有时候他们被称为2.5D

本章是在项目中刚使用3D或者2D的说明，但是尤其说了2D的开发。

## Switching Between 3D and 2D Modes
在3D和2D中切换：
1. Edit -> Project Settings -> Editor menu
2. Default Behavior Mode

## Useful 2D Project Information
无论你使用2D还是3D，这里有些有用的帮助，尤其是2D功能。

### Getting Started with Unity

### 2D Overview

### 2D Graphics

### 2D Physics

#### 2D Joints

#### 2D Collides

#### 2D Physics Material

#### 2D Effectors

## 2D vs 3D Mode Setting
2D 或者 3D模式决定了Unity编辑器中的一些设置，如下：

项目| 2D | 3D
----|------|----
导入的图片 | 假设2D，设置成Srpite  | 不假设成2D
打包工具| enabled | disabled
Scene View| 2D | 3D
默认实时光 | 没有 | 有
摄像机的位置|(0, 0, -10) | (0, 1, -10)
摄像机设置| 正交 | 透视
Skybox | disable | enable
环境因素| 颜色| 天空盒
实时GI预处理| off | on
GI 烘焙 | off | on
自动构建| off | on

