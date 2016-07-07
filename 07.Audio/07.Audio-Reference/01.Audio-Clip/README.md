# Audio Clip
声音片段包含Audio Source需要使用的音频数据。Unity支持单声道，立体声，多声道（最高支持到8个声道）。Unity可以导入.aif,wav mp3和ogg。Unity也可以导入 xm mod it 和 s3m 这些音轨格式。音轨格式的资源除了在资源监视窗口没有预览外，其他和普通的音频资源一样。

## Properties

### Load Type
Unity运行时加载音频资源的方式
* Decompress On Load: 音频文件在它们载入的时候解压。对比较小的压缩音频使用这个选项，避免性能消耗。注意解压Vorbis 编码的音效需要使用十倍的内存，所以对于大文件不要使用这个选项。
* Compressed In Memory: 保持压缩音效在内存中，然后在播放的时候解压。这个选项只有轻微的性能消耗（尤其是Ogg／Vorbis 压缩文件），所以这种模式用在大文件，因为大文件在加载的时候解压会造成太大的内存消耗。解压在合成音效线程中发生。
* Streaming: 运行时解压。这种方式使用最小的内存

### Compression Format

### Sample Rate Setting

### Force To Mono
如果打开，音频片段将会变成单一声道，并进行归一化。因为降声道往往引起声音变轻，因此适当提高了值。
### Load In Background

### Preload Audio Data

### Quality
确定压缩的数量。对PCM/ADPCM/HEVAG 格式无效。文件的大小统计可以在监视面板看到。最好的实践就是拖动进度条，确定“刚刚好”的那个点。注意这边原始尺寸指的是最初的尺寸，所以如果是个mp3文件，然后格式设置为PCM(不压缩),那么这个比例可能会大于100% 因为这个这个文件被不压缩存储占据的空间大于mp3
