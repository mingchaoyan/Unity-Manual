# Coroutines
当调用一个函数的时候，在返回前这个函数将会跑完整。所以在一个函数中的所有行为将会在一帧内执行完。函数调用不能用来完成动画或者一串事件。比如，需要渐变一个对象的alpha值
```cs
void Fade() {
    for (float f = 1f; f >= 0; f -= 0.1f) {
        Color c = renderer.material.color;
        c.a = f;
        renderer.material.color = c;
    }
}
```
以上代码并没有带来你想要的效果。为了达到渐变的效果，alpha值需要在每一帧变化。但是以上函数在一帧中执行完了，alpth值的中间值并不会在对象上出现。

把代码加到Update函数中，让渐变每帧执行当然是可以的。但是对于这种问题，用协程来处理将会比较方便。

协程类似函数，但是它可以暂停执行把控制权交给Unity然后继续在下一帧执行。在C#中协程往往这样声明：
```cs
IEnumerator Fade() {
for (float f = 1f; f >= 0; f -= 0.1f) {
    Color c = renderer.material.color;
        c.a = f;
        renderer.material.color = c;
        yield return null;
    }
}
```
有两个基本要点：1函数返回值需要为IEnumerator,2函数体中需要有yield return。yield return 那行在执行时将会被暂停然后在下一帧恢复。用StartCoroutine()函数调用协程。

Fade 函数中循环计数器在整个协程的声明周期中一直保持这正确的值，事实上任何参数或者变量都会在yield的时候保持正确的值。

协程默认会在yield的下一帧恢复，但是可以引入一个延时函数WaitForSeconds达到延时的效果。

这中方式是非常有用的优化，把效果平摊在一段时间。许多游戏中的任务需要执行，最简单的做法就是把它们都放在Update 函数中，可是Update函数会在每一秒执行多次。当一个任务不需要非常快速的回复的时候，你可以使用协程。举个例子，如果玩家旁边有的人则警告。可以把每帧检测换成每个0.1秒检测。
