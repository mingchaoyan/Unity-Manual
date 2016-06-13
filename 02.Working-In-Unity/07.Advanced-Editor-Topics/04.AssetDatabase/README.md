# AssetDatabase
AssetDatabase 是一组允许你访问你项目中的资源的API。他提供了查找，加载资源，创建，删除和修改资源的方法。Unity编辑器使用AssetDatabase在内部跟踪资源文件以及维护资源和游戏对象之间的联系。因为Unity需要跟踪项目目录的各种变化，所以你总是应该使用AssetDatabase API 而不是文件系统来访问或者改变资源数据。

AssetDatabase 接口只在编辑器中有用，在真机中没有作用。就像所有其它编辑器类一样，它只能用在Editor目录下的脚本(如果你的工程中还没有Editor目录，你需要创建一个)

## Importing an Asset
通常通过拖动资源到项目中，资源就会自动引入了，但是从脚本引入资源也是可能的。可以参看AssetDatabase.ImportAsset，以及下面例子：
```
using UnityEngine;
using UnityEditor;

public class ImportAsset {
    [MenuItem ("AssetDatabase/ImportExample")]
    static void ImportExample ()
    {
        AssetDatabase.ImportAsset("Assets/Textures/texture.jpg", ImportAssetOptions.Default);
    }
}
```
你可以通过AssetDatabase.ImportAssetOptions传入参数。脚本手册描述了不同的选项和影响。

## Loading an Asset
编辑器在需要的时候载入资源。可是，你可以使用AssetDatabase.LoadAssetAtPath,AssetDatabase.LoadMainAssetAtPath, AssetDatabase.LoadAllAssetRepresentationsAtPath和AssetDatabase.LoadAllAssetsAtPath从脚本中载入。可以在脚本文档中找到更多细节。
```
using UnityEngine;
using UnityEditor;

public class ImportAsset {
    [MenuItem ("AssetDatabase/LoadAssetExample")]
    static void ImportExample ()
    {
        Texture2D t = AssetDatabase.LoadAssetAtPath("Assets/Textures/texture.jpg", typeof(Texture2D)) as Texture2D;
    }
}
```

## File Operations using the AssetDatabase
因为Unity通过metadata来保持资源信息，所以你不应该从文件系统增加，移动或者删除资源，而是应该使用AssetDatabase.Contains, AssetDatabase.CreateAsset, AssetDatabase.CreateFolder, AssetDatabase.RenameAsset,AssetDatabase.CopyAsset,AssetDatabase.MoveAsset,AssetDatabase.MoveAssetToTrash, 和 AssetDatabase.DeleteAsset 
```
public class AssetDatabaseIOExample {
    [MenuItem ("AssetDatabase/FileOperationsExample")]
    static void Example ()
    {
        string ret;
        
        // Create
        Material material = new Material (Shader.Find("Specular"));
        AssetDatabase.CreateAsset(material, "Assets/MyMaterial.mat");
        if(AssetDatabase.Contains(material))
            Debug.Log("Material asset created");
        
        // Rename
        ret = AssetDatabase.RenameAsset("Assets/MyMaterial.mat", "MyMaterialNew");
        if(ret == "")
            Debug.Log("Material asset renamed to MyMaterialNew");
        else
            Debug.Log(ret);
        
        // Create a Folder
        ret = AssetDatabase.CreateFolder("Assets", "NewFolder");
        if(AssetDatabase.GUIDToAssetPath(ret) != "")
            Debug.Log("Folder asset created");
        else
            Debug.Log("Couldn't find the GUID for the path");
        
        // Move
        ret = AssetDatabase.MoveAsset(AssetDatabase.GetAssetPath(material), "Assets/NewFolder/MyMaterialNew.mat");
        if(ret == "")
            Debug.Log("Material asset moved to NewFolder/MyMaterialNew.mat");
        else
            Debug.Log(ret);
        
        // Copy
        if(AssetDatabase.CopyAsset(AssetDatabase.GetAssetPath(material), "Assets/MyMaterialNew.mat"))
            Debug.Log("Material asset copied as Assets/MyMaterialNew.mat");
        else
            Debug.Log("Couldn't copy the material");
        // Manually refresh the Database to inform of a change
        AssetDatabase.Refresh();
        Material MaterialCopy = AssetDatabase.LoadAssetAtPath("Assets/MyMaterialNew.mat", typeof(Material)) as Material;
        
        // Move to Trash
        if(AssetDatabase.MoveAssetToTrash(AssetDatabase.GetAssetPath(MaterialCopy)))
            Debug.Log("MaterialCopy asset moved to trash");
        
        // Delete
        if(AssetDatabase.DeleteAsset(AssetDatabase.GetAssetPath(material)))
            Debug.Log("Material asset deleted");
        if(AssetDatabase.DeleteAsset("Assets/NewFolder"))
            Debug.Log("NewFolder deleted");
        
        // Refresh the AssetDatabase after all the changes
        AssetDatabase.Refresh();
    }
}
```

## Using AssetDatabase.Refresh
当你完成资源的修改，你需要调用AssetDatabase.Refresh 来提交你的修改，并是他们在项目中可见。
