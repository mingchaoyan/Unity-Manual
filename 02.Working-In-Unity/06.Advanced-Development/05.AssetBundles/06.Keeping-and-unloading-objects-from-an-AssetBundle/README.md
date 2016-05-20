# Keeping Track of loaded AssetBundles
游戏运行时，Unity只允许你拥有一个特定的ab。如果你已经下载来一个ab并且还没有卸载，那么你不能从WWW对象中再获取一个ab。换句话说，如果你试图去访问已经加载的ab
```cs
AssetBundle bundle = www.assetBundle;
```
以下错误将会抛出
```cs
 Cannot load cached AssetBundle. A file of the same name is already loaded from another AssetBundle
```
既然如此，要么你把不用的ab卸载，要么你在内存中维护ab的引用。你可以按照自己的需要来进行。我们官方比较推荐load完对象马上把ab卸载。这样内存会干净一些，而且你也不会在load ab的时候获得报错。

注意在Unity5之前在任何bundle卸载之前，所有bundle将会加载完毕。所以待用Assetbundle.Unload 函数将会阻塞直到其它bundle加载完。这会带来性能问题，Unity5中，已经重新制作来这部分。

如果你想要对已经下载的ab跟踪，你需要使用一个包装类来管理你已经下载的ab
```cs

```
请记住，AssetBundleManager是个静态类，所以任何引用的ab将不会在载入新场景时销毁。这个类只是一个guide，正如一开始建议的，官方还是建议在使用完后unload ab ，你可以克隆一个对象来避免ab的重新load。
