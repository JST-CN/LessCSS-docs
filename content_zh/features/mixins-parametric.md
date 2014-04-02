> 如何给mixins传递参数

mixins也可以接受参数，在它进行mix in操作时会将变量传递给选择器代码块。

比如：

```less
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

接下来，你可以在系一些规则集中混入变量值：

```less
#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
```

对于这些进行mixin操作的参数也可以有默认值：


```less
.border-radius(@radius: 5px) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

然后你可以像这样调用它：

```less
#header {
  .border-radius;
}
```
这里仍然会包含一个5px的border-radius。

你也可以使用不接受参数的mixins。如果你想从输出的CSS中隐藏规则集，但是又想在其他规则集中包含它的属性，这个特性是很有用的：

```less
.wrap() {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}

pre { .wrap }
```

这会输出：

```css
pre {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}
```

### 带多个参数的mixins

参数可以用*分号*或者*逗号*分割。但是推荐使用*分号*分割。因为逗号符号有两个意思：它可以解释为mixins参数分隔符或者css列表分隔符。

使用逗号作为mixin的分隔符则无法用它创建逗号分割的参数列表。换句话说，如果编译器在mixin调用或者声明中看到至少一个分号，它会假设参数是由分号分割的，而所有的逗号都属于CSS列表:

* 两个参数，并且每个参数都是逗号分割的列表：`.name(1,2,3;something, ele)`，
* 三个参数，并且每个参数都包含一个数字：`.name(1,2,3)`，
* 使用伪造的分号创建mixin，调用的时候参数包含一个逗号分割的css列表：`.name(1,2,3;)`，
* 逗号分割默认值：`.name(@param1: red, blue)`。

定义多个具有相同名称和参数数量的mixins是合法的。Less会使用它可以应用的属性。如果使用mixin的时候只带一个参数，比如`.mixin(green)`，这个属性会导致所有的mixin都会使用强制使用这个明确的参数：


```less
.mixin(@color) {
  color-1: @color;
}
.mixin(@color; @padding:2) {
  color-2: @color;
  padding-2: @padding;
}
.mixin(@color; @padding; @margin: 2) {
  color-3: @color;
  padding-3: @padding;
  margin: @margin @margin @margin @margin;
}
.some .selector div {
  .mixin(#008000);
}
```

会编译为:

```css
.some .selector div {
  color-1: #008000;
  color-2: #008000;
  padding-2: 2;
}
```

### 命名参数

引用mixin时可以通过参数名称而不是参数的位置来为mixin提供参数值。任何参数都已通过它的名称来引用，这样就不必按照任意特定的顺序来使用参数：

```less
.mixin(@color: black; @margin: 10px; @padding: 20px) {
  color: @color;
  margin: @margin;
  padding: @padding;
}
.class1 {
  .mixin(@margin: 20px; @color: #33acfe);
}
.class2 {
  .mixin(#efca44; @padding: 40px);
}
```
会编译为：

```css
.class1 {
  color: #33acfe;
  margin: 20px;
  padding: 20px;
}
.class2 {
  color: #efca44;
  margin: 10px;
  padding: 40px;
}
```

### `@arguments` 变量

`@arguments`在mixins内部有特殊意义，调用mixin时，它包含所有传入的参数。如果你不想单个单个的处理参数，这一特性是很有用的：

```less
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}
.big-block {
  .box-shadow(2px; 5px);
}
```

返回结果为：

```css
.big-block {
  -webkit-box-shadow: 2px 5px 1px #000;
     -moz-box-shadow: 2px 5px 1px #000;
          box-shadow: 2px 5px 1px #000;
}
```

### 高级参数和`@rest`变量

如果你希望你的mixin接受数量不定的参数，你可以使用`...`。在变量名后面使用它，它会将这些参数分配给变量。

```less
.mixin(...) {        // matches 0-N arguments
.mixin() {           // matches exactly 0 arguments
.mixin(@a: 1) {      // matches 0-1 arguments
.mixin(@a: 1; ...) { // matches 0-N arguments
.mixin(@a; ...) {    // matches 1-N arguments
```

此外：

```less
.mixin(@a; @rest...) {
   // @rest 会绑定到参数 @a 之后
   // 而@arguments是绑定所有参数
}
```

## 模式匹配

有时候，你可能想要基于你传递给它的参数改变mixin的行为。先来看一些基础的示例：


```less
.mixin(@s; @color) { ... }

.class {
  .mixin(@switch; #888);
}
```

现在，比方说你想要`.mixin`基于`@switch`的值以不同的方式表现，你可这样定义这个`mixin`：


```less
.mixin(dark; @color) {
  color: darken(@color, 10%);
}
.mixin(light; @color) {
  color: lighten(@color, 10%);
}
.mixin(@_; @color) {
  display: block;
}
```

现在，如果运行它：

```less
@switch: light;

.class {
  .mixin(@switch; #888);
}
```

这将得到如下CSS：

```css
.class {
  color: #a2a2a2;
  display: block;
}
```

这里传递给`.mixin`的贪色变淡了。如果`@switch`的值是`dark`，结果会变成暗色。

这里发生了什么：

* 第一个mixin定义并没有匹配，因为它期望第一个参数是`dark`。
* 第二个mixin定义匹配了，因为它接受的参数是预期的`light`。
* 第三个mixin定义也匹配了，因为它任何值都在其预料只用。

这里只会使用匹配的mixin。变量匹配，然后绑定给任意变量。

除了变量匹配，只有一个值与其自身相等。

你也可以基于参数数量来匹配，这里有个例子：

```less
.mixin(@a) {
  color: @a;
}
.mixin(@a; @b) {
  color: fade(@a; @b);
}
```

现在，如果我们用一个参数来调用`.mixin`，这将会输出第一个定义，但是如果我们使用*两个*参数调用它，这回获取第二个定义，这就是`@a`淡入到`@b`。