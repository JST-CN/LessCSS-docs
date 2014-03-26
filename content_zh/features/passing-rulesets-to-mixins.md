> 允许在mixin中定义包装的CSS块


发布于 [v1.7.0]({{ less.master }}CHANGELOG.md)

你可能希望定义一个mixin将一个媒体查询中的一个代码块或者一个浏览器不支持的类名抽象出来。现在，你可以传递规则集给mixin，然后该mixin会包装这些规则集。比如：

```less
.desktop-and-old-ie(@rules) {
  @media screen and (min-width: 1200) { @rules(); }
  html.lt-ie9 &                       { @rules(); }
}

header {
  color: blue;

  .desktop-and-old-ie({
    background: red;
  });
}
```
这里的`desktop-and-old-ie` mixin定义了媒体查询和祖先类，因此你可以使用mixin来包装一段代码。上面这段代码会输出：

```css
header {
  background: blue;
}
@media screen and (min-width: 1200) {
  header {
    background: red;
  }
}
html.lt-ie9 header {
  background: red;
}
```

A ruleset can be now assigned to a variable or passed in to a mixin and can contain the full set of less features, e.g.

```less
@my-ruleset: {
    .my-selector {
      background-color: black;
    }
  };
```

You can even take advantage of media query bubbling, for instance

```less
@my-ruleset: {
    .my-selector {
      @media tv {
        background-color: black;
      }
    }
  };
@media (orientation:portrait) {
    @my-ruleset();
}
```

which will output

```css
@my-ruleset: {
    .my-selector {
      @media tv {
        background-color: black;
      }
    }
  };
@media (orientation:portrait) {
    @my-ruleset();
}
```