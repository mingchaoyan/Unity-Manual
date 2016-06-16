# Description of the Format
Unity 场景格式使用YAML 数据序列化语言 来实现。YAML是一个开放，免费的格式，但是这里我们不可能深层次的讲述YAML。场景中的每个对象被写进YAML文档中。注意这里所说的对象笼统指的是游戏对象，组件和其它场景数据，每个对象都需要他们自己的YAML文档。一个序列化对象的基本结构如下：

```YAML
--- !u!1 &6
GameObject:
  m_ObjectHideFlags: 0
  m_PrefabParentObject: {fileID: 0}
  m_PrefabInternal: {fileID: 0}
  importerVersion: 3
  m_Component:
  - 4: {fileID: 8}
  - 33: {fileID: 12}
  - 65: {fileID: 13}
  - 23: {fileID: 11}
  m_Layer: 0
  m_Name: Cube
  m_TagString: Untagged
  m_Icon: {fileID: 0}
  m_NavMeshLayer: 0
  m_StaticEditorFlags: 0
  m_IsActive: 1
```
第一行在文档标记之后有一个字符串"!u!1 &6"。在"!u!"后面的第一个数字指示这个对象的类型（在这个例子中 是一个GameObject）。在&符号后面的是对象id，这个id在文件中唯一，但是这个数字是任意的。每个对象的持久化属性表示为一行：
```YAML
m_Name:Cube
```
属性都以"m_"开头，然后一个脚本文档中定义的属性。文件中的第二个对象如下：
```YAML
--- !u!4 &8
Transform:
  m_ObjectHideFlags: 0
  m_PrefabParentObject: {fileID: 0}
  m_PrefabInternal: {fileID: 0}
  m_GameObject: {fileID: 6}
  m_LocalRotation: {x: 0.000000, y: 0.000000, z: 0.000000, w: 1.000000}
  m_LocalPosition: {x: -2.618721, y: 1.028581, z: 1.131627}
  m_LocalScale: {x: 1.000000, y: 1.000000, z: 1.000000}
  m_Children: []
  m_Father: {fileID: 0}
```
这是一个Transform组件，这个组件附着在前面定义的GameObject上，附属关系通过下面一句体现：
```YAML
 m_GameObject: {fileID: 6}
```
因为之前的GameObject的id是6

浮点数可以用十进制和IEEE 754格式(以0x开头)的十六进制表示。Unity没有短精度浮点数。当Unity使用十六进制的时候，它经常会在括号里协商十进制，为了调试的方便。但是只有十六进制会被解析近文件。如果你想要手动编辑这个文件，你只需要移除十六进制然后输入十进制即可。下面是合法的浮点数表示，每个值都是1.
```YAML
myValue: 0x3F800000
myValue: 1
myValue: 1.000
myValue: 0x3f800000(1)
myValue: 0.1e1
```
