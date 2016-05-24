# ShaderLab:CustomEditor
一个自定义编辑器可以定义在你的shader中。当你使用了自定义编辑器，Unity将会找这个扩展的类来扩展ShaderGUI。

## Syntax
```
CustomEditor "name"
```
 
## Details
一个自定义编辑器语句影响所有使用这个shader的材质

## Example
```
Shader "example" {
    // properties and subshaders here...
    CustomEditor "MyCustomEditor"
}
```

