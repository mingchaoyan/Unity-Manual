# Streamming Assets
Unity中大多数资源在构建的时候被合进工程。可是有时候把文件放在一个普通的文件系统中然后在目标机器上获取它们。举个例子，iOS上播放视频就需要把原始的视频文件放在文件系统中，然后使用特定函数播放。

在StreamingAssets目录中的文件将会被一字不差的拷贝到目标机器上。你可以通过Application.streamingAssetsPath来获取它们。最好总是使用这个属性来获得StreamingAssets目录，这将总是会指出正确的位置。

* 桌面系统Mac OS或者Windows
```
path = Application.dataPath + "/StreamingAssets";
```
* iOS
```
path = Application.dataPath + "/Raw";
```
* Android
```
path = "jar:file://" + Application.dataPath + "!/assets/";
```
注意在Android中，文件被压缩成jar文件（和zip压缩文件类似）。这意味着，如果你不使用Unity的WWW类来获得这个函数，那么你需要使用额外的软件来查看或者获得文件。

注意 在StreamingAssets目录的DLL文件并不参与编译。
