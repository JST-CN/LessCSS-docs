> TODO

## CSS注释

LESS保留了CSS样式注释的方法：

```less
.class {
  /* Hello, I'm a CSS-style comment */
  color: black
}
```

## LESS注释

单行注释在LESS中也是有效的，而且在编译后输出的CSS中也不会显示：

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
