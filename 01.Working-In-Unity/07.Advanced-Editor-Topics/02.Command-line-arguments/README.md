# Command line arguments
Unity经常被通过双击桌面上的图表打开，但是也可以从命令行打开。当从命令行打开时，Unity将会在开始的时候接受命令参数，这将对测试，自动构建以及其它生产任务比较有用。

在MacOS中，你可以打开Unity通过在终端输入以下：
```sh
/Applicatons/Unity/Unity.app/Contents/MacOS/Unity
```
64位Windows
```sh
 "C:\Program Files\Unity\Editor\Unity.exe"
```
32位Windows
```sh
 "C:\Program Files (x86)\Unity\Editor\Unity.exe"
```

标准的Unity将会以相同的方式启动。

## Activating Unity Silently
MacOS
```sh
 /Applications/Unity/Unity.app/Contents/MacOS/Unity -quit -batchmode -serial    R3-XXXX-XXXX-XXXX-XXXX-XXXX -username 'JoeBloggs@example.com' -password 'MyPassw0rd'
```
Windows 略

## 选项
* -logFile <pathname> 指定日志文件位置
* -executeMethod <ClassName.MethodName> 在Unity启动的时候执行一个静态方法，当asset server更新后，该工程被打开。通常这在持续集成，单元测试，构建，准备数据。当Unity抛出异常或者调用了EditorApplication.Exit时，命令行进程将会返回一个错误。你可以使用System.Environment.GetCommandLineArgs来获取传入的参数。你需要在Editor目录下放置一个合适的脚本。这个方法必须被定义为静态。
* -quit 在其它命令完成执行后，退出Unity编辑器。注意这可能导致错误消息被隐藏（但是在Editor.log 文件中会显示）
* -batchmode 以batch模式运行Unity。在与其它命令行参数结合使用的时候，这种模式应该总是被使用，因为它能保证没有弹出的窗口，不需要任何人为的干预。当执行脚本的时候发生一个异常，或者assert server更新异常，或者其它操作失败，Unity将会立即返回1。注意在batch模式中，Unity将会发送一个日志的最小版本去console。但是Log File仍然宝航来完整的日志。注意两个同样的项目雜同时以batch mode打开是不支持的，某一时刻只能打开一个Unity实例。

## 示例代码

## Unity Editor special command line arguments

## Unity Standalone Player command line arguments

## Windows Store Command line arguments
