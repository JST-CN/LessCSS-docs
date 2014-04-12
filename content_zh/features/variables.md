---
title: 变量
---

> 在一个地方管理常用的值。

## 概述(Overview)

在你的样式表中相同的值重复几十次*甚至上百次*并不少见：

```css
a,
.link {
  color: #428bca;
}
.widget {
  color: #fff;
  background: #428bca;
}
```

变量通过为你提供一种在一个地方管理这些值的方法让你的代码变得更容易维护：

```less
// 变量
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

// 用法
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```

## 变量插值(Variable Interpolation)

在上面的例子主要集中于_在CSS规则中使用变量管理值_，实际上它们还可以用在其他地方，比如选择器名称，属性名，URLs以及`@import`语句中。

### 选择器(Selectors)

版本: 1.4.0

```less
// 变量
@mySelector: banner;

// 用法
.@{mySelector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```
最终编译为：

```css
.banner {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

### URLs

```less
// 变量
@images: "../img";

// 用法
body {
  color: #444;
  background: url("@{images}/white-sand.png");
}
```

### Import语句

版本: 1.4.0

语法: `@import "@{themes}/tidal-wave.less";`

注意，目前都只有将变量声明在根作用域或者是当前作用域中，然后只有当前文件以及使用这个文件时才会考虑什么时候查找一个变量。这意味着这种用法通常在你注入变量到编译过程中或者在根文件的开始部分声明变量的做法是有限的。

当你引入一个CSS文件，同时不使用内联选项（比如，import语句保持不变）时让面的规则就不会应用。

示例：

```less
// 变量
@themes: "../../src/themes";

// 用法
@import "@{themes}/tidal-wave.less";
```

### 属性

版本: 1.6.0

```less
@property: color;

.widget {
  @{property}: #0ee;
  background-@{property}: #999;
}
```

编译为：

```css
.widget {
  color: #0ee;
  background-color: #999;
}
```

## 变量名

还可以使用变量来定义变量名：

```less
@fnord:  "I am fnord.";
@var:    "fnord";
content: @@var;
```

这会编译为：

```
content: "I am fnord.";
```

## 延迟加载

> 变量是延迟加载的，在使用前不一定要预先声明。

有效的Less片段：


```less
.lazy-eval {
  width: @var;
}

@var: @a;
@a: 9%;
```
下面这个也是有效的Less片段：

```less
.lazy-eval-scope {
  width: @var;
  @a: 9%;
}

@var: @a;
@a: 100%;
```
最终都会编译为：

```css
.lazy-eval-scope {
  width: 9%;
}
```

在定义一个变量两次时，只会使用最后定义的变量，Less会从当前作用域中向上搜索。这个行为类似于CSS的定义中始终使用最后定义的属性值。

比如：

```less
@var: 0;
.class1 {
  @var: 1;
  .class {
    @var: 2;
    three: @var;
    @var: 3;
  }
  one: @var;
}
```
会编译为：

```css
.class1 .class {
  three: 3;
}
.class {
  one: 1;
}
```

## 默认变量

有时候你会用到默认变量-让你能够在没有设置某些变量的情况下设置指定的变量。这一特性并不强制要求你这么做，因为你可以很容易通过插入后定义同名变量的方式覆盖默认变量。

比如：

```less
// library
@base-color: green;
@dark-color: darken(@base-color, 10%);

// use of library
@import "library.less";
@base-color: red;
```
这个是能够工作的 - 其中base-color会被重写，而dark-color依然是暗红色。