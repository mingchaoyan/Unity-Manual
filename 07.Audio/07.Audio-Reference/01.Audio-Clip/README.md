# Audio Clip
声音片段包含Audio Source需要使用的音频数据。Unity支持单声道，立体声，多声道（最高支持到8个声道）。Unity可以导入.aif,wav mp3和ogg。Unity也可以导入 xm mod it 和 s3m 这些音轨格式。音轨格式的资源除了在资源监视窗口没有预览外，其他和普通的音频资源一样。

## Properties

### Load Type
Unity运行时加载音频资源的方式
* Decompress On Load: 音频文件在它们载入的时候解压。较小的音效文件可以使用这个选项来避免在运行时解压的消耗。注意在加载的时候解压Vorbis编码的音频资源将会带来大约10倍的内存消耗（ADPCM大约3.5倍）,所以如果是大文件不要用这个选项。
* Compressed In Memory: 保持压缩音效在内存中，然后在播放的时候解压。这个选项只有轻微的性能消耗（尤其是Ogg／Vorbis 压缩文件），所以这种模式用在大文件，因为大文件在加载的时候解压会造成太大的内存消耗。解压在合成音效线程中发生。
* Streaming: 运行时解压。这种方式使用最小的内存来缓冲压缩数据，运行时逐渐从磁盘中读入然后解压。注意解缩在单独的线程中进行。

### Compression Format
音频文件使用时的压缩格式。注意根据当前选择的构建目标会有不同的选项。
* PCM 该选项在非常耗文件大小的前提下提供了比较高质量的音质。
* ADPCM 这个格式对于一些有一点噪音但是需要非常大的数量的音效有用，比如脚步，冲撞声，武器声。它的压缩比比PCM小3.5倍。但是CPU消耗也是比较小。
* Vorbis/MP3 压缩成比较小的文件，但是相比较PCM有一点音质上的损失。压缩比例可以根据滑动条来调节。这个格式对于中等长度的音效和背景音乐比较合适。
* HEVAG PS专用格式。

### Sample Rate Setting
PCM和ADPCM压缩格式允许自动优化活着手动优化冗余采样
* Preserve Sample Rate 默认情况下，保证设置样本不变；
* Optimize Sample Rate 自动优化采样率
* Override Sample Rate 手动修改采样率

### Force To Mono
如果打开，音频片段将会变成单一声道，并进行归一化。因为降声道往往引起声音变轻，因此适当提高了值。

### Load In Background
如果打开，音频片段将会在后台加载而不阻塞住主线程。默认这个是关闭的，用来确保Unity的默认行为：所有音频文件在场景开始之前会完成加载。注意音频的播放清酒将会延迟直到加载完成。可以根据AudioClip.loadState 属性来查看当前的加载状态。

### Preload Audio Data
如果打开，音频文件将会在场景加载前提前加载。这是Unity默认的行为。如果这个标志没有被设置，那么音频文件警徽在第一次 AudioSource.Play() 或者 AudioSource.PlayOneShot() ，或者通过AudioSource.LoadAudioData() 或者通过 AudioSource.UnloadAudioDat() 卸载。

### Quality
确定压缩的数量。对PCM/ADPCM/HEVAG 格式无效。文件的大小统计可以在监视面板看到。最好的实践就是拖动进度条，确定“刚刚好”的那个点。注意这边原始尺寸指的是最初的尺寸，所以如果是个mp3文件，然后格式设置为PCM(不压缩),那么这个比例可能会大于100% 因为这个这个文件被不压缩存储占据的空间大于mp3

## Preview Window
预览窗口包含三个icon
* 选中的时候就播放
* 循环
* 播放


## Importing Audio Assets
Unity 可以读取非常多的文件格式，无论何时被文件被导入的时候，它都会根据构建目标被转成合适的格式和类型。这些也是可选的通过inspector界面。

一般情况下，PCM和和Vorbis/MP3格式会被优先使用，因为比较接近原始资源。PCM对CPU要求非常轻量级，因为声音将是无压缩以及能够从内存直接读取，Vorbis/MP3会根据质量滑动条来损失合适的数据。

ADPCM 是一种在CPU和内存中的折衷，它比未压缩的PCM选项CPU消耗多一点,但是少了将近3.5倍的内存，虽然这个内存大小还是比是使用Vobis和MP3压缩多出3倍。 关于ADPCM（PCM）允许自动优化或者手动设置样本比例——这取决于声音内容的频率以及可以接受的有损率——这能进一步减少音频资源的体积。

模块文件（mod it s3m xm）可以使用非常低的空间的带来非常高质量。当使用模块文件的，除非你特殊需要，确保Load Type 被设置为Compressed In Memroy

一般来说，压缩格式最好用来比较长的文件，比如背景音乐或者对话，而PCM或者ADPCM比较适合用在端音效上。你需要微调压缩比率。直到刚刚好的情况。

## Platform specific details
### iOS/Android
在移动平台上，音频片段被编码为Voribs 除非显式的设置为MP3
