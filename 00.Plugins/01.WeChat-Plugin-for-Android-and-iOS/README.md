# WeChat Plugin for Android and iOS - An easier solution for integrating WeChat share to your games

## What is WeChat Plugin for Android an iOS
微信插件是一个帮助你在安卓和iOS平台上使用微信分享的Unity包。你可以在不编写代码只是把按钮绑定到我们的对象上完成设置分享。

## Main features:
* 非常简单的设置，包括场景对象的设置。
* C# 脚本和 原生插件都包含在内。
* 支持分享音乐，视频，链接，文本，图片。

## Set Up Guide
如果你是从WeChatPluginAndriod升级上来的，请看Upgrade Guide部分。
设置的最重要的事情是在http://developers.wechat.com/ 网站上注册和获得批准。微信的英文支持网站是非常令人讨厌的，有很多错误。所以我建议在中文网站注册：https://open.weixin.qq.com/ 。注册完以后创建一个app。记下App Id。
当你已经注册了你的应用然后获得微信的确认。下载然后导入WeChatPluginAndriodIOS 进你的项目文件
如果你的项目已经有AndroidManifest. 你可以删除这个，然后添加下面几行：
在"<application"标签前添加：
```
<uses-permission android:name="android.permission.INTERNET" />

<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS"/>

<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
1. 把 WeCahtPluginAndroidIOS/Prefab/WeCahtPluginAndroidIOS.prefab 拖到你想要分享的场景中。
2. 把你的AppID填入
3. 设置你需要分享的内容，使用prefab编辑器。下面有文档说明。
4. 在你的按钮脚本上添加 WeChatPluginScript对象的引用。
5. 调用share.<变量名>.Share();
6. 确保你的项目包名在微信网站傻姑娘注册过

如果你只计划设置iOS，那么现在就可以愉快地去分享了。
如果是安卓：
1. 使用在WeChatPluginAndroidIOS/Source.zip中过的app_signatures.apk 安装在你的设备中。
2. 然后安装你应用在同样的设备中。
3. 打开app_signatures app 然后从你的应用中获取签名。
4. 在微信网站上设置你的应用的签名。
5. 恭喜你，现在可以分享了。

以上就是设置的全部内容。
下面看看示例程序。

## Demo Example 
有一个示例程序来帮助你开始使用WeChatPluginAndroidIOS。你可以打开 在WeChatPluginAndroidIOS/Demo目录下的DemoScene来运行。在这个示例中，你可以获得基本的认识，WeChatPluginAndroid对不同类型的分享。你可以跟着DemoScript.cs来设置你的自定义选项。当然不要忘记有WeChatPluginAndorid 与肢体可以用。

## WeChatPluginAndroidIOS Editor configuration definitions
* App ID 从微信网站注册获取的应用ID
* Is Moments 勾选需要分享到朋友圈，不勾选就是分享给微信上的某个朋友。
* Share Type 需要分享的类型，提供以下类型：图片，链接，文本，音乐，视频
* Image Sharing Type  从用户设备中分享图片，从链接中分享图片，从纹理中分享图片
* Thumb Type 从用户设备中分享图片，从链接中分享图片，从纹理中分享图片

## FAQ
当分享的时候，啥都没发生，哪里出问题了：
A. 如果一点都没发生：
 * 很多事情可能导致分享失败；
 * 检查liabmmsdk.jar 是否在Plugs/Android目录下 以及 是否正确配置
 * 检查WeChatPlugin.jar 是否在Plugs/Android目录下 以及 是否正确配置
 * 使用的纹理并没有被设置成可读写
 * 微信没有安装
B. 如果微信打开了，然后又关闭了
 * 非常重要：你的应用可能没有被微信批准，你需要去微信网站上批准。
 * 你可能没有设置对你的包名
 * 你可能没有设置好签名
 * 在脚本中，你可能没有设置好app ID 
 * 当你分享图片的时候发生错误
 * 设置纹理为Read/Write Enable 然后RGBA 32 格式
 
## Upgrad Guide
如果你是从WeChatAndroidPlugin升级上来的，请删掉以下文件来确保升级没有问题：
* WeChatPluginAndroid 目录以及内容
* Editor/WeChatPluginAndroid 目录以及内容


