### color

> 解析颜色，将代表颜色的字符串转换为颜色值。

参数： `string`: 代表颜色值的字符串。

返回： `color`

示例： `color("#aaa");`

输出： `#aaa`


### convert

> 将数字从一种类型转换到另一种类型。

第一个参数为带单位的数值，第二个参数为单位。如果两个参数的单位是兼容的，则数字的单位被转换。如果两个参数的单位不兼容，则原样返回第一个参数。

无需转化改变单位参照 [unit](#misc-functions-unit)。

_兼容的单位组_:

* 长度: `m`, `cm`, `mm`, `in`, `pt` and `pc`,
* 时间: `s` and `ms`,
* 角度: `rad`, `deg`, `grad` and `turn`.

参数：
* `number`: 带单位的浮点数。
* `identifier`, `string` or `escaped value`: 单位

返回： `number`

示例：

```less
convert(9s, "ms")
convert(14cm, mm)
convert(8, mm) // 不兼容的单位类型
```

输出：

```
9000ms
140mm
8
```


### data-uri

> 将一个资源内嵌到样式文件，如果开启了ieCompat选项，而且资源文件的体积过大，或者是在浏览器中使用，则会使用`url()`进行回退。如果没有指定MIME，则Node.js会使用MIME包来决定正确的MIME。

参数：
* `mimetype`: 可选参数，MIME类型字符串。
* `url`: 需要内嵌的文件的URL。

示例： `data-uri('../data/image.jpg');`

输出： `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

在浏览器中输出： `url('../data/image.jpg');`

示例： `data-uri('image/jpeg;base64', '../data/image.jpg');`

输出： `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

### default

> 只能边界条件中使用，没有匹配到其他自定义函数（mixin）的时候返回`true`，否则返回`false`。

示例：

```less
.mixin(1)                   {x: 11}
.mixin(2)                   {y: 22}
.mixin(@x) when (default()) {z: @x}

div {
  .mixin(3);
}

div.special {
  .mixin(1);
}
```
输出：

```css
div {
  z: 3;
}
div.special {
  x: 11;
}
```

`default`的返回值还可以和边界操作一起使用。例如，`.mixin() when not(default()) {}`，将会在至少一个除自身外的自定义函数(mixin)满足条件时被调用：

```less
.mixin(@value) when (ispixel(@value)) {width: @value}
.mixin(@value) when not(default())    {padding: (@value / 5)}

div-1 {
  .mixin(100px);
}

div-2 {
  /* ... */
  .mixin(100%);
}
```
结果：

```css
div-1 {
  width: 100px;
  padding: 20px;
}
div-2 {
  /* ... */
}
```

在同一个边界条件或者不同的混合条件中，`default()`可以被调用多次：

```less
div {
  .m(@x) when (default()), not(default())    {always: @x}
  .m(@x) when (default()) and not(default()) {never:  @x}

  .m(1); // OK
}
```
然而，使用`default()`时如果检测到多个混合条件有*潜在性*冲突，Less会抛出一个异常：

```less
div {
  .m(@x) when (default())    {}
  .m(@x) when not(default()) {}

  .m(1); // Error
}
```
在以上的例子中，通过与其他条件的相互依赖就可以确认在调用时`default()`所返回的值。

更多`default()`的高级用法：

```less
.x {
  .m(red)                                    {case-1: darkred}
  .m(blue)                                   {case-2: darkblue}
  .m(@x) when (iscolor(@x)) and (default())  {default-color: @x}
  .m('foo')                                  {case-1: I am 'foo'}
  .m('bar')                                  {case-2: I am 'bar'}
  .m(@x) when (isstring(@x)) and (default()) {default-string: and I am the default}

  &-blue  {.m(blue)}
  &-green {.m(green)}
  &-foo   {.m('foo')}
  &-baz   {.m('baz')}
}
```
结果：

```css
.x-blue {
  case-2: #00008b;
}
.x-green {
  default-color: #008000;
}
.x-foo {
  case-1: I am 'foo';
}
.x-baz {
  default-string: and I am the default;
}
```

`default`函数只能作为Less构建函数_在边界条件_中使用。如果在混合条件之外使用，`default`函数只会被解释成普通的CSS属性值：

示例：

```less
div {
  foo: default();
  bar: default(42);
}
```
结果：

```css
div {
  foo: default();
  bar: default(42);
}
```


### unit

> 移除或者改变属性值的单位。

参数：
* `dimension`: 数字，带或不带单位。
* `unit`: 可选参数，将要替换成的单位，如果省略则移除原单位。

转化成指定单位参照 [convert](#misc-functions-convert)。

示例： `unit(5, px)`

输出： `5px`

示例： `unit(5em)`

输出： `5`