> 带条件的mixins。

当你想要匹配_表达式_，而不是简单的值或者参数数量时，guard是很有用的。如果你熟悉函数式编程，那么你肯定遇到过这类问题。

为了尽可能的保持CSS声明的本质，Less选择实现了**guarded mixins**，而不是`if`/`else`语句，也就是说并不是一脉相承的实现`@media`查询的规范。

让我们从一个例子开始：

```less
.mixin (@a) when (lightness(@a) >= 50%) {
  background-color: black;
}
.mixin (@a) when (lightness(@a) < 50%) {
  background-color: white;
}
.mixin (@a) {
  color: @a;
}
```

这里有一个`when`关键字，它引进了一个guard序列（在这里只有一个guard）。现在，假设我们运行以下代码：

```less
.class1 { .mixin(#ddd) }
.class2 { .mixin(#555) }
```

会得到：

```css
.class1 {
  background-color: black;
  color: #ddd;
}
.class2 {
  background-color: white;
  color: #555;
}
```

### Guard中的比较运算符

guards中可用的比较运算符的完整列表为： `>`, `>=`, `=`, `=<`, `<`。此外，关键字`true`是让两个mixins等价的唯一真值：

```less
.truth (@a) when (@a) { ... }
.truth (@a) when (@a = true) { ... }
```

除了关键字`true`，其他任何值都是假值：

```less
.class {
  .truth(40); // Will not match any of the above definitions.
}
```
Guards可以使用逗号`,`分割，如果guards求值都为`true`，它就被认为是一个相等的匹配：

```less
.mixin (@a) when (@a > 10), (@a < -10) { ... }
```

注意，你也可以比较其他每个参数或者不使用参数：

```less
@media: mobile;

.mixin (@a) when (@media = mobile) { ... }
.mixin (@a) when (@media = desktop) { ... }

.max (@a; @b) when (@a > @b) { width: @a }
.max (@a; @b) when (@a < @b) { width: @b }
```

### 类型检查函数

最后，如果你想基于值类型匹配mixins，那么你可以使用`is`函数：

```less
.mixin (@a; @b: 0) when (isnumber(@b)) { ... }
.mixin (@a; @b: black) when (iscolor(@b)) { ... }
```

下面是一些基本的类型检查函数：

* `iscolor`
* `isnumber`
* `isstring`
* `iskeyword`
* `isurl`

如果你想检查一个值除了数字是否是一个特定的单位，你可以使用下列方法之一：

* `ispixel`
* `ispercentage`
* `isem`
* `isunit`

### 带条件的mixins

_(**FIXME**)_ 此外，`default`函数可以用于让一个mixin匹配依赖于其他mixin匹配，然后你可以使用它来创建类似于`else`或者`default`语句（分别属于`if`和`case`结构）的“条件式mixins”：

```less
.mixin (@a) when (@a > 0) { ...  }
.mixin (@a) when (default()) { ... } // matches only if first mixin does not, i.e. when @a <= 0
```
最后一项要点，在一个guard内你可以使用`and`关键字提供额外的条件：

```less
.mixin (@a) when (isnumber(@a)) and (@a > 0) { ... }
```

最后，**`not`**关键字用于否定条件：

```less
.mixin (@b) when not (@b > 0) { ... }
```