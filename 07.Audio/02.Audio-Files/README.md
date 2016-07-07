# Audio Files
就像网格和纹理那样，音频资源的工作流非常平滑。对于音频文件，Unity能够导入几乎所有格式的文件，但是仍然有些注意点值得提一下。

从Unity5.0开始，音频数据与实际的声音片段分离。音频数据仅仅是一个包括实际声音数据文件的引用，在音频数据中有很多运行时的选项。这意味着你有非常大的自由度来决定哪些音频资源应该在内存中一直保留(因为你预先无法预知它们将会多频繁的被播放，比如脚步声，武器声音，或者撞击声)，哪些资源仅仅需要在使用的时候加载(比如语音对话，背景音乐，环境音乐循环)。

当音效被编码以后存储的选项无非就是PCM,ADPCM和Compressed。不同的平台也有不同的格式，但是它们工作方式相似。Unity 支持很多常用格式，默认的模式是压缩，这样音频数据在各个平台是被压缩的。

查看AudioClip 文档来获取详细的压缩格式信息和其他可用的编码数据。
TODO

## Supported Formats
Format	Extensions
MPEG layer 3	.mp3
Ogg Vorbis	.ogg
Microsoft Wave	.wav
Audio Interchange File Format	.aiff / .aif
Ultimate Soundtracker module	.mod
Impulse Tracker module	.it
Scream Tracker module	.s3m
FastTracker 2 module	.xm
