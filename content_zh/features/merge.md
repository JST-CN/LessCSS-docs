> 合并属性

`merge`特性可以从多个属性中将值集合集合到一个单一属性之下的逗号或空格分割属性列表中。对于诸如background和transform之类的属性来说，`merge`非常有用。

## 逗号

> 通过逗号添加属性的值

发布于 [v1.5.0]({{ less.master }}CHANGELOG.md)

示例：

```less
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}
```
输出：

```css
.myclass {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}
```

## Space

> Append property value with space

Released [v1.7.0]({{ less.master }}CHANGELOG.md)

Example:

```less
.mixin() {
  transform+_: scale(2);
}
.myclass {
  .mixin();
  transform+_: rotate(15deg);
}
```
Outputs

```css
.myclass {
  transform: scale(2) rotate(15deg);
}
```


为避免任何非有意的添加，`merge`需要在每个待加入的声明中显示的设置一个`+`或者`+_`标记。

_注意：尽管transform规范中属性使用空格分割，但它仍然支持使用逗号分割；这也是为什么这个特性中没有选项来配置用空格还是逗号分割的原因。_
