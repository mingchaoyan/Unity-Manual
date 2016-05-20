# Asset Bundle Internal Structure
一个AssetBundle是在序列化文件中的一组物体。场景的bundle和普通bundle在内部资源组织上有略微差别。

## 普通格式

## 场景格式

## 压缩
chunk based 压缩格式：原数据被分割成子块，单独压缩。随机读取的消耗比较小。
stream based 压缩格式：整块压缩，提供了高的压缩比但是不支持串行读。



