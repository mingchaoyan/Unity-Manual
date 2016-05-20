# Loading and unloading objects from an AssetBundle
加载有三种方式：
1. AssetBundle.LoadAsset
2. AssetBundle.LoadAssetAsync 不会block主线程
3. AssetBundle.LoadAllAssets 会加载所有包含在AB中的对象

卸载资源可以使用AssetBundle.Unload。传false保留已经load的对象，传true彻底释放内存，包括已经加载的资源。

## Loading objects from an AssetBundles asynchronously
可以使用AssetBundle.LoadAssetAsync方法来异步加载资源，从而避免游戏卡顿
```cs
using UnityEngine;

// Note: This example does not check for errors. Please look at the example in the DownloadingAssetBundles section for more information
IEnumerator Start () {
    // Start a download of the given URL
    WWW www = WWW.LoadFromCacheOrDownload (url, 1);

    // Wait for download to complete
    yield return www;

    // Load and retrieve the AssetBundle
    AssetBundle bundle = www.assetBundle;

    // Load the object asynchronously
    AssetBundleRequest request = bundle.LoadAssetAsync ("myObject", typeof(GameObject));

    // Wait for completion
    yield return request;

    // Get the reference to the loaded object
    GameObject obj = request.asset as GameObject;

    // Unload the AssetBundles compressed contents to conserve memory
    bundle.Unload(false);

    // Frees the memory from the web stream
    www.Dispose();
}
```
