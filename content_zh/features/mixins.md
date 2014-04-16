> 从现有的样式混合（mixin）属性

你可以混合“类”选择器或者“id”选择器，例如：
```less
.a, #b {
  color: red;
}
.mixin-class {
  .a();
}
.mixin-id {
  #b();
}
```
以上将得到:
```css
.a, #b {
  color: red;
}
.mixin-class {
  color: red;
}
.mixin-id {
  color: red;
}
```

*（小提示：当你调用混合集的时候，括号可加可不加）*

```less
.a();   //这两种调用方式效果是一样的
.a;
```

## 不输出混合集

如果你想要创建一个混合集，但是却不想让它输出到你的样式中，你可以在混合集的名字后面加上一个括号。
```less
.my-mixin {
  color: black;
}
.my-other-mixin() {
  background: white;
}
.class {
  .my-mixin;
  .my-other-mixin;
}
```
结果为：

```css
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
```

## 带选择器的混合集

混合集不仅可以包含各种属性，而且可以包括各种选择器。

例如：

```less
.my-hover-mixin() {
  &:hover {
    border: 1px solid red;
  }
}
button {
  .my-hover-mixin();
}
```

结果为：

```css
button:hover {
  border: 1px solid red;
}
```

## 命名空间

如果你想要将属性混合到比较复杂的选择器中，你可以通过嵌套多层id或者class。

```less
#outer {
  .inner {
    color: red;
  }
}

.c {
  #outer > .inner;
}
```

同样 `>` 是可选的

```less
// 下面四种写法效果是一样的
#outer > .inner;
#outer > .inner();
#outer.inner;
#outer.inner();
```

这种用法的效果相当于我们熟知的命名空间，你可以把混合集放到一个id选择器里面，这样可以确保它（这个混合集）不会跟其他的库冲突。

例如：

```less
#my-library {
  .my-mixin() {
    color: black;
  }
}
// 可以这样调用
.class {
  #my-library > .my-mixin();
}
```

## `!important` 关键字

在调用的混合集后面追加 `!important` 关键字，可以使混合集里面的所有属性都继承 `!important`：

例如：

```less
.foo (@bg: #f5f5f5, @color: #900) {
  background: @bg;
  color: @color;
}
.unimportant {
  .foo();
}
.important {
  .foo() !important;
}
```

结果为:

```css
.unimportant {
  background: #f5f5f5;
  color: #900;
}
.important {
  background: #f5f5f5 !important;
  color: #900 !important;
}
```
