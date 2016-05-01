# Loading Resources at Runtime
有些情况下，虽然资源并不是场景的一部分，但是也需要能被加载。如能在每个场景中出现的角色但是出现的情况又是比较罕见的（比如一个隐藏的彩蛋，错误消息，最高记录消息）。更进一步，为了缩短首次下载的时间或者动态更新游戏内容，你需要一种可以从其他文件加载资源的机制。
Unity支持需要时再加载的资源目录。你可以创建Asset Bundles，这些和游戏文件完全分离，你可以从文件或者URL上按需下载。

## Asset Bundles
一个Asset Bundle是一个资源的集合。你可以有很多Asset Bundles，这些文件存在于编好的Unity包外面，通常会在一个Web服务器上以供玩家动态下载。

你可以在编辑器脚本中使用BuildPipeline.BuildAssetBundles()来构建AssetBundle，你可以使用数组作为参数指定需要编进AB文件的资源。之后你可以用，AssetBundle.LoadAsset()在运行时动态加载资源。

## 资源目录
资源目录里放了虽然还没有被连接到在Inspector窗口中的GameObject但是确实包含在游戏里的一些资源。

在Project 视图中新建一个命名为Resources的目录，接着你就可以组织各种不同的资源目录，无论使用哪个目录下的，都可以调用Ressource.Load()

如果你目标部署在Streaming Web上，你可以指定一个场景包含资源目录中所有内容，可以在设置作用设置。Stream 队列由构建时的顺序决定。

注意：所有在Resources目录下的资源以及他们的依赖关系都被保存在一个脚仔resources.assets的文件中。设置可以指定

如果某个关卡先于“Frist streamed Level”，这些资源将会被存在这个关卡中，如果是之后的关卡，那么引用resources.assets中的资源

只有在Resources目录下的资源才可以被Resources.Load()加载，但是其他很多资源也会被存在resource.assets中，因为他们有依赖关系（比如说一个在Resources目录下的材质可能指定了在Resources目录外的一个纹理）

## 资源卸载
可以使用AssetBundle.Unload 卸载AB资源，如果给unloadAllLoadedObjects传true参数，所有AB内部持有的对象和通过AssetBundle.LoadAsset()载入的对象都会在内存中被销毁。

有时候你更希望加载AB，实力化一个游戏对象，释放AB所占用的空间。这样的好处是你可以给其他任务腾出更多内存（比如载入另一个AB），这种情况下你可以传false参数，当AB在内存中销毁之后，你就再也不能从这个AB中加载对象了。

如果你想要销毁一个从Resouce.Load（）中加载的场景对象，可以使用Object.Destry()。使用Resources.UnloadUnusedAssets()释放资源。
