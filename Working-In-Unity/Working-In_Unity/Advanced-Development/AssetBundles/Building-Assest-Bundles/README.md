# Building Asset Bundles
创建一个ab首先需要选中它。在inspector窗口底部可以指定。

资源默认的AB option是None，这意味着这个机缘将不会被写入任何一个AB中，而是整体打包在项目中。

AB的名字是小写的，使用斜杠（forward slash）将创建一个目录

## 使用BuildPipeline.BuildAssetBundle导出
0. 在Inspector底部标记本资源需要打包进的AB
1. BuildPipeline.BuildAssetBundle打包已经被标记的资源
2. 确保已经创建AssetBundles目录

```cs
using UnityEditor;

public class CreateAssetBundles
{
    [MenuItem ("Assets/Build AssetBundles")]
    static void BuildAllAssetBundles ()
    {
        BuildPipeline.BuildAssetBundles ("AssetBundles");
    }
}
```

每一个ab都有一个对应的manifest，这里面包含了CRC冗余校验，资源依赖等信息。

## AB 编辑器工具
### 使用AssetDatabase.GetAllAssetBundleNames获取AB名字
```cs
using UnityEditor;
using UnityEngine;

public class GetAssetBundleNames
{
    [MenuItem ("Assets/Get AssetBundle names")]
    static void GetNames ()
    {
        var names = AssetDatabase.GetAllAssetBundleNames();
        foreach (var name in names)
        Debug.Log ("AssetBundle: " + name);
    }
}
```

### 使用OnPostprocessAssetbundleNameChanged告知开发者,资源改变了AB
```CS
using UnityEngine;
using UnityEditor;

public class MyPostprocessor : AssetPostprocessor {
    void OnPostprocessAssetbundleNameChanged ( string path, string previous, string next)
    { 
        Debug.Log("AB: " + path + " old: " + previous + " new: " + next); 
    } 
}
```

####  AssetBundle 变量
可以指定"my_assets.hd" "my_assets.sd" 这两个内部id一致，但可以分别获取。

### 一堆API

