# Importing Assets
在Unity外部创建的资源必须通过保存在Assets目录或者直接复制进Assets目录。对于大多数格式来说，你可以直接保存源文件进Assets目录，Unity能够识别它。当改变的时候，Unity也会通知需要重新导入。

当你创建了一个Unity工程，你实际上创建了一个以你工程名字命名的目录－这个目录中包含了以下子目录：Assets， Libarary， obj， ProjectSettings
Assts目录是你应该保存资源的地方。

Project 窗口的内容也是显示你Assets目录下的内容。所以，当你复制或者保存文件到Assets 目录的时候，这个文件将会在Project 窗口中被看到。

Unity将会自动检测被加到Assets目录的文件。当你把任何资源放到Assets目录的时候，你就能在Project中看到。

当你把文件从你电脑的文件系统中拖到Project窗口，效果也一样。

Project上看到你文件（大部分情况）就是你电脑上的文件，如果你在Unity上删了它，你也就在你的电脑上删了它。

上图显示了一个简单的例子：文件和Unity工程中的Assets 目录。你可以组织很多类似的。

你注意到有些.meta文件列在你的文件系统中但是却没有显示在Unity Project窗口中。Unity为每个资源和目录创建.meta文件，但是他们默认是隐藏的。所以你可能不能在Exploer/Finder看到。

meta文件包含许多关于资源怎么在项目中使用的信息，所以他们必须和资源文件关联，所以当你重命名或者移动一个资源文件的时候，你必须同时对meta文件做相应的操作。

最简单地移动或者重命名你的资源的方式就是总是在Unity编辑器项目中指向。这种情况下，Unity将会自动移动或者重命名相应的meta文件。如果你愿意，behind-the-scenes-during-the-import-process页面将会有更多信息。

如果你想要带一堆资源进你的项目，你可以使用Asset Packages。

## Some common type of Asset

### Image files

最常见的图片格式都被支持，比如BMP，TIF， TGA，JPG以及PSD，如果你保存了ps的图层进你的Assets目录，它们会被导入为压平的文件。你可以在importing－images－with－alpha－channels－from－photoshop，或者 importing－your－images－as－sprites页面上获得更多信息。

### 3D 模型文件

如果你从常见的3D软件中保存它们原始的格式（.max,.blend,.mb.ma）进Assets目录，它们会调用你3D FBX导出插件。所以你可以选择在你的3D软件中导出FBX，然后导入Unity。

### Meshes & Animations

无论什么3D包你在使用，Unity将会导入它们的mesh和动画。

你的mesh文件不需要一个动画被导入。如果你使用动画，你可以选择从单个文件导入动画，或者你从不同的分割的文件中导入。更多信息，参阅手册。

### Audio Files

如果你导入并没有压缩过的音效，它们将会按照指定的压缩格式导入。

### Other Asset Types

所有的情况，你的原始文件将不会被Unity修改，即使在Unity中你经常可以选择多种压缩格式，修改，或者在其它情况下处理资源。导入程序读取你的源文件，然后创建一个游戏读取内部资源，来匹配你的设置。如果你修改了导入设置，或者修改了原始文件，这将会导致Unity重导资源来实现你新的改变。

注意，导入原始的3D格式，需要在同一台机器上安装有3D软件。因为Unity使用3D软件的FBX导出插件来读取文件。或者你可以选择直接导出成FBX然后保存进Unity项目。
