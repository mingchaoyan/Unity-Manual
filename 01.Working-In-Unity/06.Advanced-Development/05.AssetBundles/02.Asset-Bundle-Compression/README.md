# Asset Bundle Compression
Unity 支持三种压缩AB的方式：LZMA，LZ4，不压缩
* LZMA
默认的压缩格式。这种压缩格式是一个单独的LZMZ流的串行化数据文件，在使用之前需要被解压。

LZMA压缩的bundles给予尽可能小的体积，但是相对的解压会比较慢，导致载入时间显得比较慢。

* LZ4 
Unity也支持LZ4压缩，这会导致比较大的压缩文件体积，但是在使用之前并不需要完全解压。LZ4是一个基于 chunk的算法，当需要的对象从LZ4压缩的bundle解压的时候，对应的对象部分被解压。这将会比较快，在使用之前几乎不用等待解压的时间。LZ4格式在5.3被引进，之前的版本并不支持。

* 不压缩格式
第三种完全不压缩。这种bundles非常大，但是在下载使用的时候最快。

## Caching of Compressed Bundles

WWW.LoadFromCacheOrDownload 函数下载并缓存assetbundles到磁盘上，这样可以加速之后的下载。从5.3开始，cached数据用LZ4压缩。这样节约了大约40%-60%的空间（对比不压缩）。重新压缩发生在下载的时候，用户几乎不会察觉。但数据从socket中出来，Unity会解压然后重新把它压成LZ4格式。重新压缩发生在下载的时候，也就是说当数据一够就开始压缩，知道下载完成。之后数据也是在需要时被按照chunks解压。

Cache压缩被Caching.compressionEnabled属性控制。他影响在磁盘和内存中的bundles。

## AssetBundle load API overview
下表比较了使用不同load方式的内存，性能等方面


## 兼容性
为了支持新的压缩格式以及为之后的功能做基础，ab的格式不断的变化。Unity5仍然支持Unity4创建的budle，但是不支持4之前的bundle。

