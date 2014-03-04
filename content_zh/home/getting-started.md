---
标题: 开始准备
---

Less 是一个Css 预编译器,意思指的是它可以扩展Css语言,添加功能如允许变量(variables),混合(mixins),函数(functions) 和许多其他的技术，让你的Css更具维护性，主题性，扩展性。

Less 可运行在 Node 环境,浏览器环境和Rhino环境.同时也有3种可选工具供你编译文件和监视任何改变。

例如:

```less
@base: #f938ab;

.box-shadow(@style, @c) when (iscolor(@c)) {
  -webkit-box-shadow: @style @c;
  box-shadow:         @style @c;
}
.box-shadow(@style, @alpha: 50%) when (isnumber(@alpha)) {
  .box-shadow(@style, rgba(0, 0, 0, @alpha));
}
.box {
  color: saturate(@base, 5%);
  border-color: lighten(@base, 30%);
  div { .box-shadow(0 0 5px, 30%) }
}
```

编译后

```css
.box {
  color: #fe33ac;
  border-color: #fdcdea;
}
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```
