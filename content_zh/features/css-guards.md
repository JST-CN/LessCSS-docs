> 类似"if"形式的选择器

发布于 [v1.5.0]({{ less.master }}CHANGELOG.md)

约束也适用于CSS选择器，这是一个声明mixin的语法糖，会立即调用它。

例如，在1.5.0之前你不得不这样做。

```less
.my-optional-style() when (@my-option = true) {
  button {
    color: white;
  }
}
.my-optional-style();
```
现在你可以直接在样式上编写约束。

```less
button when (@my-option = true) {
  color: white;
}
```
你还可以通过与`&`特性结合实现'if'类型的语句，从而允许组合多个约束。

```less
& when (@my-option = true) {
  button {
    color: white;
  }
  a {
    color: blue;
  }
}
```
