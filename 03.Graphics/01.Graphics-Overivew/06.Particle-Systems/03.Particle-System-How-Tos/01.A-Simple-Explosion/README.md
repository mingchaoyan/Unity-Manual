# A Simple Explosion
你可以使用粒子系统创建一个比较真实的爆炸，但是过程啃根比看到它的第一样要复杂。核心上来说，爆炸只是一个向外喷射的粒子，但是你可以做出不少改动使他看起来更加真实。

## Timeline of a Particle
一个爆炸产生一个球状的火焰，飞速的向外飞。初始的爆炸能量非常巨大而且非常灼热运行非常快速。能量迅速消失导致火焰慢下来，冷却下来。最后等到所有燃料燃烧殆尽，火焰迅速消失。

一个爆炸通常有一个比较短的生命线，你可以在生命线中改变很多值模拟效果。粒子一开始移动非常快然后速度迅速降低。同样，颜色也从一开始非常明亮逐渐变暗。最后缩小粒子的大小达到燃料燃尽火焰消失的效果。

## 实现
使用默认的粒子系统object
Shape module Sphere，0.5unit in redius
Renderer Fire 关掉Cast Shadows，Receive Shadows

目前，该粒子系统看起来想恒多小火从中点扔了出去。当然，爆炸应该制造爆炸感。
Emission module Rate 0 
