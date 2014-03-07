> 编写循环

在Less中，混合可以调用它自身。这样，当一个混合递归调用自己，再结合[Guard表达式](#mixin-guards-feature)和[模式匹配](#mixins-parametric-feature-pattern-matching)这两个特性，就可以写出循环结构。

示例：

```less
.loop(@counter) when (@counter > 0) {
  .loop((@counter - 1));    // 递归调用自身
  width: (10px * @counter); // 每次调用时产生的样式代码
}

div {
  .loop(5); // 调用循环
}
```

输出：

```css
div {
  width: 10px;
  width: 20px;
  width: 30px;
  width: 40px;
  width: 50px;
}
```

使用递归循环最常见的情况就是生成栅格系统的CSS：

```less
.generate-columns(4);

.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
```

输出：

```css
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
```
