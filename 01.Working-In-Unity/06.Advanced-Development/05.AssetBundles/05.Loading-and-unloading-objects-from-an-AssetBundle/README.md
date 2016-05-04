# Loading and unloading objects from an AssetBundle
加载有三种方式：
1. AssetBundle.LoadAsset
2. AssetBundle.LoadAssetAsync 不会block主线程
3. AssetBundle.LoadAllAssets 会加载所有包含在AB中的对象

卸载资源可以使用AssetBundle.Unload。传false保留已经load的对象，传true彻底释放内存，包括已经加载的资源。


