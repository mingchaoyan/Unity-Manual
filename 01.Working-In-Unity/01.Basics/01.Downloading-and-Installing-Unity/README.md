# Downloading and Installing Unity

你能够从Unity官网上下载安装Unity 编辑器

使用Download Assistant安装器来操作（如果你想要使用torrent来下载Unity编辑器或者同时安装Unity的多个版本，你可以查看在下面的 通过Torrent 下载）

## Unity Download Assistant

从Unity5.0开始，一个将近1M的Unity下载器使你可以选择Unity的组件。如果你不知道你需要哪些组件你可以使用默认的选择点击Continue。

## Installing Unity without the Download Assistant
如果你喜欢下载格子的Unity组件，而不使用Downlad Assistant。每个组件都是一个常见的可执行文件，所以如你你是Unity 新手你会发现使用Download Assistans 是比较简单的。有些公司中的开发中，比如希望可以自动部署Unity的，可能希望在命令行安装Unity

### Installing Unity on Windows from comand line
略

### Installing Unity on OS X fro command line
Unity的安装器是一个.pkg文件，可以使用下面的步骤使用安装器。

#### Unity Editor install
在目标卷的/Applications/Unity目录下
```
sudo installer [-dumplog] -pakgage Unity.pkg -target /
```

#### Web Player install
Web player 安装在/Library/Internet-Plug-ins/Unity Web Player.plugin 
```
sudo installer [-dumplog] -package StandardAssets.pkg -target /
```

#### Standard Assets install
安装在/APpications/Unity/Standard Assets/
```
sudo installer [-dumplog] -package StandarAssets.pkg -target /
```

#### Example Project install
 安装在/Users/Shared/Unity/Standard-Assets 
 ```
 sudo installer [-dumplog] -package Examples.pkg -target /
 ```

 ## Torrent Download
 如果你更喜欢通过BitTorrent客户端下载Unity，你可以在我的的 download archive page 页面中找到种子链接。注意不是所有版本都有种子链接，如果可以使用将会在下载下拉菜单中显示。

 ## 同时安装
你可以在同一个电脑上安装你想要多少就多少unity版本。Mac版本的安装器将会创建一个一个叫做"Unity"的目录，如果该目录已经存在，将会覆盖它。可是如果你重命名了这个目录，那么两个版本将会愉快地共存在同一个电脑中。在PC上，安装器总会命名"Unity X.Y.z(fp)W",这种类似官方的发布，p是补丁版本。

我们强烈建议你谨慎地重命名一个目录。注意所有现存的快捷键，别名以及离线文档的链接都将不再指向老版本的Unity。对于离线文档来说这将会尤其困惑，你会发现你浏览器上的离线文档的书签不可用了，这时候你应该去检查书签指向的URL。

