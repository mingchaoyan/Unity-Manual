# Storing and loading binary data in an AssetBundle

首先把你的数据文件以.bytes扩展名保存。Unity 就会把这个当作TextAsset。TextAsset格式的文件可以被打进AssetBundle。当你下载AB以后，加载TextAsset对象，你就可以使用.bytes熟悉来获取文本对象。
