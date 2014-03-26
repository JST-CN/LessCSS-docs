> 从mixin中返回变量

所有定义在一个mixin中的变量都是可见的，还可以用于调用它的作用域中（除非调用它的作用域定义了同名变量）。

示例：

```less
.mixin() {
  @width:  100%;
  @height: 200px;
}

.caller {
  .mixin();
  width:  @width;
  height: @height;
}

```
结果：

```css
.caller {
  width:  100%;
  height: 200px;
}
```
因此定义在mixin中的变量还可以充当它的返回值。这样就允许我们创建一个用起来类似函数的mixin。

示例：

```less
.average(@x, @y) {
  @average: ((@x + @y) / 2);
}

div {
  .average(16px, 50px); // "call" the mixin
  padding: @average;    // use its "return" value
}
```

结果：

```css
div {
  padding: 33px;
}
```