---
title: 特性概览
---

> 作为一种 CSS 扩展, Less 不仅向后兼容 CSS, 它还使用现有的 CSS 语法新增了额外的特性. 这使得学习 Less 更轻松, 一旦有任何问题，可以随时退回使用标准的 CSS.


### 变量(Variables)

顾名思义:

```less
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header {
  color: @light-blue;
}
```

输出:

```css
#header {
  color: #6c94be;
}
```

注意，由于变量只能定义一次，实际上他们就是“常量”.


### 混合(Mixins)

混合就是一种将一系列属性从一个规则集引入(“混合”)到另一个规则集的方式。假设我们有以下 `class`:

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

我们希望在另一个规则集内部使用上面这些属性。那么，我们就只需要访问我们想要的属性所在类的名称即可，就像下面这样：

```less
#menu a {
  color: #111;
  .bordered;
}

.post a {
  color: red;
  .bordered;
}
```

类 `.bordered` 的属性现在就会同时呈现在 `#menu a` 和 `.post a` 中（注意，同样可以将 `#ids` 作为 mixins）。

**Learn more**

* [More about mixins](#mixins-feature)
* [Parametric Mixins](#mixins-parametric-feature)


### 嵌套规则(Nested rules)

Less 为我们提供了嵌套的能力, 而不是合并在样式表中.假设我们有下面的 CSS:

```css
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

在 Less 中，我们可以以下面这种方式编写:

```less
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```

这样的代码更简洁, 它模仿了 HTML 的结构.

使用这种方法照样可以在混合中包含伪类(pseudo-selectors)。下面是一个经典的 clearfix 代码，在这里使用 mixin 重写了（`&` 表示当前选择器的父选择器）:

```less
.clearfix {
  display: block;
  zoom: 1;

  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```

**See also**

* [Parent Selectors](#parent-selectors-feature)

### 运算(Operations)

任何数值，颜色和变量都可以进行运算。这里有一对示例：

```less
@base: 5%;
@filler: @base * 2;
@other: @base + @filler;

color: #888 / 4;
background-color: @base-color + #111;
height: 100% / 2 + @filler;
```

最后的输出结果与你预期的一样 -- Less 能够推断颜色和单位之间的区别。如果在一个运算中使用了单位，比如：

```less
@var: 1px + 5;
```
在这个例子中 Less 会在最终输出结果中使用这个单位 -- `6px`。

### 函数(Functions)

Less 提供了许多用于转换颜色，处理字符串和进行算术运算的函数。他们在函数参考一节有详细的的介绍。

这些函数使用起来非常简单。在下面的例子中我们使用 `percentage` 将 0.5 转换为 50%，然后将基础颜色值的饱和度增加了 5%，最后将背景颜色的亮度增加了 25% 之后又将色相值增加 8:

```less
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```


### 命名空间和访问器(Namespaces & Accessors)

(不要将它与 [CSS `@namespace`](http://www.w3.org/TR/css3-namespace/) or [namespace 选择器](http://www.w3.org/TR/css3-selectors/#typenmsp)混为一谈)。

有时候，出于组织的目的，或者为了提供一些封装，你会希望将你的变量和 mixins 组合在一起。在 Less 中做到这一点非常直观，假设你想在 `#bundle` 下捆绑一些 mixins 和变量，以便稍候复用或者分发：

```less
#bundle {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab { ... }
  .citation { ... }
}
```

现在如果我们想在 `#header a` 中混合 `.button` 类，那么我们可以这样做：

```less
#header a {
  color: orange;
  #bundle > .button;
}
```


### 作用域(Scope)

Less 中的作用域与编程语言中的作用域概念非常相似。首先会在局部查找变量和混合，如果没找到，编译器就会在父作用域中查找，依次类推。

```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```

变量和混合不必在使用前声明，因此下面的代码与前面的例子等价：

```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```

**See also**

* [Lazy Loading](#variables-feature-lazy-loading)


### 注释(Comments)

可以使用块注释和行注释:

```less
/* One hell of a block
style comment! */
@var: red;

// Get in line!
@var: white;
```

### 导入(Importing)

导入工作与你预期的一样。你可以导入一个 `.less` 文件，然后这个文件中的所有变量都可以使用了。对于 `.less` 文件而言，其扩展名是可选的。

```css
@import "library"; // library.less
@import "typo.css";
```
