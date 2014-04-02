> extend是一个Less伪类，它会合并它所在的选择其和它所匹配的引用。


发布于 [v1.4.0]({{ less.master }}CHANGELOG.md)

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
```
在上面设置的规则中，`:extend`选择器会在*`.inline`类出现的地方*在`.inline`上应用"扩展选择器"(也就是`nav ul`)。声明块保持原样，不会带有任何引用扩展(因为扩展并不是CSS)。

因此下面的代码：

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
.inline {
  color: red;
}
```

输出：

```css
nav ul {
  background: blue;
}
.inline,
nav ul {
  color: red;
}
```

注意`nav ul:extend(.inline)`选择器是如何输出得到`nav ul`的 - 输出之前移除了扩展，然后选择器块保持不变。如果代码块中没有放入属性，则从输入中移除它（但是扩展仍然会影响其他选择器）。

## 扩展语法(extend语法)
extend可以附加给一个选择器，也可以放入一个规则集中。它看起来像是一个带选择器参数伪类，也可以使用关键字`all`选择相邻的选择器。

示例：

```less
.a:extend(.b) {}

// 上面的代码块与下面这个做一样的事情
.a {
  &:extend(.b);
}
```

```less
.c:extend(.d all) {
  // 扩展".d"的所有实例，比如".x.d"或者".d.x"
}
.c:extend(.d) {
  // 扩展选择器输出为".d"的唯一实例
}
```

它可以包含多个要扩展的类，使用逗号分割即可。

示例：

```less
.e:extend(.f) {}
.e:extend(.g) {}

// 上面的代码与下面的做一样的事情
.e:extend(.f, .g) {}
```

### 为选择器附加扩展

给选择器附加扩展看起来就像一个普通的带参数的伪类选择器。一个选择器可以包含多个扩展分支，但是所有的扩展都必须在选择器的尾部。

* 选择器之后的扩展：`pre:hover:extend(div pre)`。
* 在选择器和扩展之间有空格是允许的：`pre:hover :extend(div pre)`.
* 也允许有多个扩展: `pre:hover:extend(div pre):extend(.bucket tr)` - 注意这与 `pre:hover:extend(div pre, .bucket tr)`一样。
* 这是不允许的: `pre:hover:extend(div pre).nth-child(odd)`。因为扩展必须在最后。

如果一个规则集包含多个选择器，所有选择器都可以使用extend关键字。下面演示了一个规则集中多个带extend的选择器：

```less
.big-division,
.big-bag:extend(.bag),
.big-bucket:extend(.bucket) {
  // body
}
```

### 规则集内的extend

也可以使用`&:extend(selector)`语法在规则集内置入extend。将extend放入规则集内是一种将它放入单个规则选择器的快捷方式。

规则内的extend：

```less
pre:hover,
.some-class {
  &:extend(div pre);
}
```
与给每个选择器添加一个extend完全相同：

```less
pre:hover:extend(div pre),
.some-class:extend(div pre) {}
```

### 嵌套选择器中的extend

extend还可以匹配嵌套选择器，比如有下面的Less：

示例：

```less
.bucket {
  tr { // 目标选择器中的嵌套规则
    color: blue;
  }
}
.some-class:extend(.bucket tr) {} // 识别嵌套规则
```
这会输出：

```css
.bucket tr,
.some-class {
  color: blue;
}
```
从本质上将extend会查找编译后的CSS，而不是原始的less。

示例：

```less
.bucket {
  tr & { // 目标选择器中的嵌套
    color: blue;
  }
}
.some-class:extend(tr .bucket) {} // 识别嵌套规则
```

输出：

```css
tr .bucket,
.some-class {
  color: blue;
}
```


### extend中的精确匹配

Extend默认会在选择器之间寻找精确匹配。它不管选择器是以星号开始还是不是。它也不管两个nth表达式是否具有相同的意义，它们必须以相同的形式匹配。唯一例外的是属性选择器中的引号，less会知道它们是相同的，然后匹配它。

示例：

```less
.a.class,
.class.a,
.class > .a {
  color: blue;
}
.test:extend(.class) {} // 不会匹配上面的任何选择器的值
```

*号开头也是有关系的。选贼起`*.class`和`.class`是等价的，而extend不会匹配它们：

```less
*.class {
  color: blue;
}
.noStar:extend(.class) {} 不会匹配*.class选择器
```

输出：

```css
*.class {
  color: blue;
}
```

伪类的顺序是有关系的。选择器`link:hover:visited`和`link:visited:hover`匹配相同的元素集合，但是extend会区别对待它们：

```less
link:hover:visited {
  color: blue;
}
.selector:extend(link:visited:hover) {}
```
输出：

```css
link:hover:visited {
  color: blue;
}
```

### nth表达式

Nth形式的表达式也是有关系的。Nth表达式`1n+3`和`n+3`是等价的，但是extend并不能匹配它们：

```less
:nth-child(1n+3) {
  color: blue;
}
.child:extend(n+3) {}
```
输出：

```css
:nth-child(1n+3) {
  color: blue;
}
```

属性选择器中的引号类型也是有关系的。以下所有都是等价的：


```less
[title=identifier] {
  color: blue;
}
[title='identifier'] {
  color: blue;
}
[title="identifier"] {
  color: blue;
}

.noQuote:extend([title=identifier]) {}
.singleQuote:extend([title='identifier']) {}
.doubleQuote:extend([title="identifier"]) {}
```
输出

```css
[title=identifier],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title='identifier'],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title="identifier"],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}
```

## Extend "all"

当你在extend参数的最后面指定all关键字时，它会告诉告诉匹配作为其他选择器一部分的选择器。这个选择器会被复制，然后匹配的选择器部分会使用扩展替换，创建一个新的选择器。

示例：

```less
.a.b.test,
.test.c {
  color: orange;
}
.test {
  &:hover {
    color: green;
  }
}

.replacement:extend(.test all) {}
```

输出：

```css
.a.b.test,
.test.c,
.a.b.replacement,
.replacement.c {
  color: orange;
}
.test:hover,
.replacement:hover {
  color: green;
}
```

_你可以认为这种操作模式就是无损搜索和替换。_


### Extend中的选择器插值

> Extend不能匹配变量选择器。如果选择器包含变量，extend会忽略它。

这是一个悬而未决的特性，改变它并不容易。然而，extend可以附加给插值选择器。

带变量的选择器不会匹配：

```less
@variable: .bucket;
@{variable} { // 插值选择器
  color: blue;
}
.some-class:extend(.bucket) {} // 找不到匹配
```

同时在extend中使用目标选择器变量也什么都不匹配：

```less
.bucket {
  color: blue;
}
.some-class:extend(@{variable}) {} // 插值选择器什么也不匹配
@variable: .bucket;
```

上面两个例子都会编译为：

```less
.bucket {
  color: blue;
}
```

然而, `:extend` 附加给插值选择器是能够工作的：

```less
.bucket {
  color: blue;
}
@{variable}:extend(.bucket) {}
@variable: .selector;
```

上面的例子会编译为：

```less
.bucket, .selector {
  color: blue;
}
```

## 作用域/@media内的extend

编写在media声明内的extend也应该只匹配同一media声明内的选择器：

```less
@media print {
  .screenClass:extend(.selector) {} // media内的extend
  .selector { // 这个会匹配到-因为在同一的media内
    color: black;
  }
}
.selector { // 定义样式表中的规则 - extend会忽略它
  color: red;
}
@media screen {
  .selector {  // 另一个media声明内的规则 - extend也会忽略它
    color: blue;
  }
}
```

最终编译为：

```css
@media print {
  .selector,
  .screenClass { /*  同一media内的规则扩展成功 */
    color: black;
  }
}
.selector { /* 定义样式表中的规则被忽略 */
  color: red;
}
@media screen {
  .selector { /* 其他media中的规则也被忽略 */
    color: blue;
  }
}
```
编写在media声明内的extend不会匹配嵌套声明内的选择器：

```less
@media screen {
  .screenClass:extend(.selector) {} // media内的extend
  @media (min-width: 1023px) {
    .selector {  // 嵌套media内的规则 - extend会忽略它
      color: blue;
    }
  }
}
```

编译为：

```css
@media screen and (min-width: 1023px) {
  .selector { /* 其他嵌套media内的规则被忽略 */
    color: blue;
  }
}
```
顶级extend匹配一切，包括media嵌套内的选择器：

```less
@media screen {
  .selector {  /* media嵌套内的规则 - 顶级extend正常工作 */
    color: blue;
  }
  @media (min-width: 1023px) {
    .selector {  /* media嵌套内的规则 - 顶级extend正常工作 */
      color: blue;
    }
  }
}

.topLevel:extend(.selector) {} /* 顶级extend匹配一切 */
```

编译为：

```css
@media screen {
  .selector,
  .topLevel { /* media嵌套内的规则被扩展了 */
    color: blue;
  }
}
@media screen and (min-width: 1023px) {
  .selector,
  .topLevel { /* media嵌套内的规则被扩展了 */
    color: blue;
  }
}
```

### 检测重复

现在，这里还没有检测重复。

示例：

```less
.alert-info,
.widget {
  /* declarations */
}

.alert:extend(.alert-info, .widget) {}
```
输出：

```css
.alert-info,
.widget,
.alert,
.alert {
  /* declarations */
}
```

## Extend用例

### 经典用例

经典用于就是避免添加基础类。比如，如果你有：

```css
.animal {
  background-color: black;
  color: white;
}
```
如果你想有一个animal子类型，并且要重写背景颜色。那么你有两个选择，首先改变你的HTML

```html
<a class="animal bear">Bear</a>
```
```css
.animal {
  background-color: black;
  color: white;
}
.bear {
  background-color: brown;
}
```

或者简化HTML，然后在你的less中使用extend，比如：

```html
<a class="bear">Bear</a>
```

```less
.animal {
  background-color: black;
  color: white;
}
.bear {
  &:extend(.animal);
  background-color: brown;
}
```

### CSS尺寸归并

Mixins会复制所有的属性到选择器中，这可能导致不必要的重复。因此你可以使用extend来代替mixin将你要用的属性移过去，这样就会生成更少的CSS。

mixin示例：

```less
.my-inline-block() {
    display: inline-block;
  font-size: 0;
}
.thing1 {
  .my-inline-block;
}
.thing2 {
  .my-inline-block;
}
```

输出：

```css
.thing1 {
  display: inline-block;
  font-size: 0;
}
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

extend示例：

```less
.my-inline-block {
  display: inline-block;
  font-size: 0;
}
.thing1 {
  &:extend(.my-inline-block);
}
.thing2 {
  &:extend(.my-inline-block);
}
```

输出：

```css
.my-inline-block,
.thing1,
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

### 合并样式/更高级的mixin

另一个用例可以用作mixin的替代 - 因为mixin仅仅能用于简单的选择器，如果你的html中有两个不同的块，但是你需要为这两个块应用相同的样式，那么你可以使用extend来关联这两块。

示例：

```less
li.list > a {
  // list styles
}
button.list-style {
  &:extend(li.list > a); // 使用相同的列表样式
}
```