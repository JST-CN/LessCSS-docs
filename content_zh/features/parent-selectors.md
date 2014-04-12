> 使用`&`引用父选择器

`&`运算符表示一个嵌套规则的父选择器，它在应用修改类或者应用伪类给现有选择器时最常用：

```less
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```

结果为：

```css
a {
  color: blue;
}

a:hover {
  color: green;
}
```

注意，如果上面的示例没有使用`&`，那么它的结果就是`a :hover`（一个匹配`<a>`标签内的hovered元素的后代选择器），这通常并不是我么想要的嵌套的`:hover`的结果。

“父选择器”有各种各样的用法。基本上，任何时候你都需要以不同的方式来组合选择器嵌套的规则，而不是默认规则。比如，一个使用`&`的典型的场景就是生成重复的类名：

```less
.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
```

输出：

```css
.button-ok {
  background-image: url("ok.png");
}
.button-cancel {
  background-image: url("cancel.png");
}
.button-custom {
  background-image: url("custom.png");
}
```

### 多个 `&`

`&`可以在一个选择器中出现不止一次。这就使得它可以反复引用父选择器，而不是重复父选择器的类名。

```less
.link {
  & + & {
    color: red;
  }

  & & {
    color: green;
  }

  && {
    color: blue;
  }

  &, &ish {
    color: cyan;
  }
}
```

这会输出：

```css
.link + .link {
  color: red;
}
.link .link {
  color: green;
}
.link.link {
  color: blue;
}
.link, .linkish {
  color: cyan;
}
```

注意，`&`代表所有的父选择器（而不只是最近的长辈），因此下面的例子：

```less
.grand {
  .parent {
    & > & {
      color: red;
    }

    & & {
      color: green;
    }

    && {
      color: blue;
    }

    &, &ish {
      color: cyan;
    }
  }
}
```

结果为：

```css
.grand .parent > .grand .parent {
  color: red;
}
.grand .parent .grand .parent {
  color: green;
}
.grand .parent.grand .parent {
  color: blue;
}
.grand .parent,
.grand .parentish {
  color: cyan;
}
```


### 改变选择器顺序

要前置插入一个选择器给继承的(父)选择器时它是很有用的。用过将`&`放到当前选择器之后就可以做到这一点。

比如，使用Modernizr时，你可能希望基于要支持的特性来指定不同的规则：

```less
.header {
  .menu {
    border-radius: 5px;
    .no-borderradius & {
      background-image: url('images/button-background.png');
    }
  }
}
```

选择器`.no-borderradius &`会前置插入`.no-borderradius`给它的父选择器`.header .menu`，最后变成`.no-borderradius .header .menu`形式输出：

```css
.header .menu {
  border-radius: 5px;
}
.no-borderradius .header .menu {
  background-image: url('images/button-background.png');
}
```


### 组合使用(explosion->爆发?)

`&`还可以用于生成一个逗号分割列表的所有可能的选择器排列：


```less
p, a, ul, li {
border-top: 2px dotted #366;
  & + & {
      border-top: 0;
  }
}
```
这个组合可以扩展出指定元素的所有（16种）可能的组合：

```css
p,
a,
ul,
li {
  border-top: 2px dotted #366;
}
p + p,
p + a,
p + ul,
p + li,
a + p,
a + a,
a + ul,
a + li,
ul + p,
ul + a,
ul + ul,
ul + li,
li + p,
li + a,
li + ul,
li + li {
  border-top: 0;
}
```