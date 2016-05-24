# ShaderLab:Fallback
在所有子shader之后定义了一个Fallback。大致的意思是：“如果以上没有子shader，那么试着使用这个shader”

## Syntax
```
Fallback "name"
```
定义了一个fallback

```
Fallback Off
```

显式声明了即使没有子shader可以在硬件上跑也没有fallback以及没有警告需要显示

## Details
一个fallback声明就像其它shader中的subshader插入到这里。

## Example
``` 
Shader "example" {
    // properties and subshaders here...
    Fallback "otherexample"
}
```
