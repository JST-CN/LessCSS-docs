> TODO

## CSS注释

CSS 的注释格式在 LESS 中依然有效：

```less
.class {
  /* Hello, I'm a CSS-style comment */
  color: black
}
```

## LESS注释

LESS 同样也支持双斜线的注释，但是编译成 CSS 的时候自动过滤掉：

```less
.class {
  // Hi, I'm a silent comment, I won't show up in your CSS
  color: white
}
```

{{#todo}}
* document `/*! ... */`
* document and/or link to `--s0`/`--s1` options
{{/todo}}
