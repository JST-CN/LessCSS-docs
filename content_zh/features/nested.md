> Less允许你使用嵌套以及标准的层叠CSS。

...

### 嵌套媒体查询

媒体查询可以如同选择器一样嵌套，它会创建输出合适的媒体查询规则。

比如：

```less
.one {
  @media (width: 400px) {
    font-size: 1.2em;
    @media print and color {
      color: blue;
    }
  }
}
```

这会输出：

```css
@media (width: 400px) {
  .one {
    font-size: 1.2em;
  }
}
@media (width: 400px) and print and color {
  .one {
    color: blue;
  }
}
```

...

### `&` 和mixin

`&`连接符还可以用于mixins。在用于mixin的情况下，`&`引用的是它被混入的类所在作用域中的选择器。

比如：

```less
.mixin {
  &:hover {
    color:cyan;
  }
}
.blue {
  .mixin;
  color:blue;
}

```

输出：

```css
.mixin:hover {
  color: cyan;
}

.blue {
  color: blue;
}
.blue:hover {
  color: cyan;
}
```
