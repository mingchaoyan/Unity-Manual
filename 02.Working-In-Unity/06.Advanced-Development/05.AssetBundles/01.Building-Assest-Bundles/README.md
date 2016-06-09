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

##  AssetBundle 变量
可以指定"my_assets.hd" "my_assets.sd" 这两个内部id一致，但可以分别获取。

## 脚本建议
### API to mark the asset into AssetBundle
你可以使用AssetImporter.assetBundlename 来设置AssetBundle的名字

### Simple APIs
BuildPipeline.BuildAssetBundles() 是可用来构建AssetBundle的简单API。你只需要提供：
* AssetBundles 的输出路径
* 描述构建AssetBundle的编译选项
* 构建目标
* 同时也有一个重载版本提供AssetBundle的数组。

### APIs to manipulate AssetBundle names in the asset database
AssetDatabase.GetAllAssetBundleNames() 返回在资源数据库中的所有AssetBundle 名字
AssetDatabase.GetAssetPathsFromAssetBundle() 返回给定AssetBundle中标记的资源路径
AssetDatabase.RemoveAssetBundleName() 移除资源数据库中给定的AssetBundle名字
AssetDatabase.GetUnusedAssetBundleName() 返回没有使用的AssetBundle名字
AssetDatabase.RemoveUnusedAssetBundleNames() 移除资源库中所有没有使用的资源
AssetPostProcessor.OnPostprocessAssetbundleNameChanged() 在用户改变AssetBundle名字的的时候回调

### BuildAssetBundleOptions
CollectDependencies and DeterministicAssetBundle 始终打开
CompleteAsset 5.0中始终打开
ForceRebuildAssetBundle 即使没有改变，你也会强制重新构建AssetBundle
IngoreTypeAssetBundle 即使类型树改变了，你可以忽略
DisableWriteTypeTree 和 IngorTypeTreeChanges 冲突。如果你关掉了 type tree 你就不能ignore type tree change

### Minifest file
每个AssetBundle都会有一个对应的清单文件，它包含以下内容：
* 每个AssetBundle一个Minifest file
* CRC
* 资源文件 hash 一个单一的hash，只用来做构建检查
* 类型树 hash 一个单一的hash ，用来做构建检查
* Clsss type  这个AssetBundle中所有的类。使用单一的hash 当构建时
* Asset name 在Assetbundle所有的资源
* Dependent AssetBundle name 这个Assetbundle所依赖的所有资源
* 这些清单文件只是构建的时候有用，在运行时是不必要的

### Sigle manifest file
我们夜生成了一个单一的清单文件，它包含：
* 所有的AssetBundle
* 所有的依赖

### Sigle manifest AssetBundle
包含一个AssetBundleMnifest对象，包含以下API:
* GetAllAssetBundles() 返回这次构建所有的AssetBundle
* GetDircetDependencies() 返回直接依赖的assetbundle名字
* GetAssetBundleHash 返回指定AssetBundle的hash
* GetAllAssetBundleWithWariant() 返回所有带变量的AssetBundle

### AssetBundle lading APIs changed
* AssetBundle.GetAllAssetNames() 返回在AssetBundle中所有的资源名称
* AssetBundle.GetAllScenePaths()  返回所有的场景资源路径
* AssetBundle.LoadAsset() 从AssetBundle加载资源
* AssetBundle.LoadAllAssets().
* AssetBundle.LoadAssetWithSubAssets().
* 异步版本也同样提供
* 组件的类型不再返回。可以通过先加载GameObject然后在这个对象上找组件

### Typetrees
默认的一个AssetBundle会有一个typetree。
