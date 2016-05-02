# Downloading AssetBundles

两种方法下载AB
1. 无缓存：创建一个WWW对象，AB不会被Unity的Cache目录缓存
2. 有缓存：WWW.LoadFromCacheOrDownload，AB会被Cache在Unity的Cache目录。Web Player能最多cache50MB，PC/Mac或者iOS／Android的限制是4GB。其他平台参阅脚本文档。


