# Downloading AssetBundles

本部分假设你已经学会了如何构建ab；

两种方法下载AB
1. 无缓存：创建一个WWW对象，AB不会被Unity的本地Cache目录缓存
2. 有缓存：WWW.LoadFromCacheOrDownload，AB会被Cache在Unity的Cache目录。Web Player能最多cache50MB，PC/Mac或者iOS／Android的限制是4GB。其他平台参阅脚本文档。

无缓存的下载例子
```cs
using System;
using UnityEngine;
using System.Collections; 
class NonCachingLoadExample : MonoBehaviour {
    public string BundleURL;
    public string AssetName;
    IEnumerator Start() {
        // Download the file from the URL. It will not be saved in the Cache
        using (WWW www = new WWW(BundleURL)) {
            yield return www;
            if (www.error != null)
                throw new Exception("WWW download had an error:" + www.error);
            AssetBundle bundle = www.assetBundle;
            if (AssetName == "")
                Instantiate(bundle.mainAsset);
            else
                Instantiate(bundle.LoadAsset(AssetName));
            // Unload the AssetBundles compressed contents to conserve memory
            bundle.Unload(false);
        } // memory is freed from the web stream (www.Dispose() gets called implicitly)
    }
}
```

有缓存
```cs
using System;
using UnityEngine;
using System.Collections;

public class CachingLoadExample : MonoBehaviour {
    public string BundleURL;
    public string AssetName;
    public int version;

    void Start() {
        StartCoroutine (DownloadAndCache());
    }

    IEnumerator DownloadAndCache (){
        // Wait for the Caching system to be ready
        while (!Caching.ready)
            yield return null;

        // Load the AssetBundle file from Cache if it exists with the same version or download and store it in the cache
        using(WWW www = WWW.LoadFromCacheOrDownload (BundleURL, version)){
            yield return www;
            if (www.error != null)
                throw new Exception("WWW download had an error:" + www.error);
            AssetBundle bundle = www.assetBundle;
            if (AssetName == "")
                Instantiate(bundle.mainAsset);
            else
                Instantiate(bundle.LoadAsset(AssetName));
                    // Unload the AssetBundles compressed contents to conserve memory
                    bundle.Unload(false);

        } // memory is freed from the web stream (www.Dispose() gets called implicitly)
    }
}
```
当你访问.assetBundle的时候，下载数据已经被提取，ab已经创建。所以这时候你可以加载这个bundle中的对象。LoadFromCacheOrDownload 函数的第二个参数指定了下载那个ab。当AB并没有在cache中出现，或者cache中的版本比较小，LoadFromCacheOrDownload 将会下载ab，否则ab会从cache中加载。

注意当使用WWW.LoadFromCacheOrDownload的时候每帧只有一个ab能完成。

## 放在一起
现在已有的组件已经可以让你创建一个场景，然后加载你的ab，并在屏幕上显示出来。

## Loading AssetBundles in the Editor
当编辑器中使用ab，需要构建加载，这些会降低开发进程。比如一个ab中的资源被修改，然后这会导致整个ab需要重打。在生产环境中，很有可能导致所有ab都重新构建，这导致一个ab的修改需要很长的操作。一个比较好的方式是在代码中有分开的路径在编辑器中直接使用资源而不是使用ab。可以使用Resources.LoadAssetAtPath
```cs
// C# Example
// Loading an Asset from disk instead of loading from an AssetBundle
// when running in the Editor
using System.Collections;
using UnityEngine;

class LoadAssetFromAssetBundle : MonoBehaviour
{
    public Object Obj;

    public IEnumerator DownloadAssetBundle<T>(string asset, string url, int version) where T : Object {
        Obj = null;

#if UNITY_EDITOR
        Obj = Resources.LoadAssetAtPath("Assets/" + asset, typeof(T));
        yield return null;

#else
        // Wait for the Caching system to be ready
        while (!Caching.ready)
            yield return null;

        // Start the download
        using(WWW www = WWW.LoadFromCacheOrDownload (url, version)){
            yield return www;
            if (www.error != null)
                        throw new Exception("WWW download:" + www.error);
            AssetBundle assetBundle = www.assetBundle;
            Obj = assetBundle.LoadAsset(asset, typeof(T));
            // Unload the AssetBundles compressed contents to conserve memory
            bundle.Unload(false);

        } // memory is freed from the web stream (www.Dispose() gets called implicitly)

#endif
    }
}
```
