data-URI是一个bash脚本，它的作用是把文件夹中所有的PNG图片放到一个LESS文件中，这么做的目的是为了在主LESS文件中引用这个包含全部图片base64编码以及尺寸的LESS文件。

```bash
#!/bin/bash

SRC="$1"
DST="$2"
TMP="$(mktemp)"

find "$SRC" -name "*.png" | while read i; do
    j="$(basename "$i")"
    f="$(echo "${j%.png}" | tr "@#&%+-. " "_")"
    echo "@gfx_$f: \"data:$(file -b --mime-type "$i");base64,$(base64 -w0 "$i")\";"
    echo "@size_$f: $(gm identify -format "%wpx %hpx" "$i" 2>/dev/null);"
done > "$TMP";
mv "$TMP" "$DST"
```

根据你的设置，可以修改`mktemp`,`file`,`base64`和`gm` [GraphicsMagick]的路径或参数。

在源文件夹中会有2张由脚本生成的PNG图片，`foo.png`和`foo@2x.png`（base64编码能节省空间）：

```less
@foo-img: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB0AAAAfCAYAAAA(...)";
@foo-size: 29px 31px;
@foo-img-2x: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADoAAAA+CAYA(...)";
@foo-size-2x: 58px 62px;
```

也可以像下面的例子一样创建LESS文件:

```less
@import "gfx.less" //脚本生成的LESS文件

.foo {
  background: url(@foo-img) no-repeat center center;
  -webkit-background-size: @size-foo;
}

@media only screen and (-webkit-min-device-pixel-ratio: 2) {
  .foo {
    background-image: url(@foo-img_2x);
  }
}
```

data-URI能提高代码的加载速度，还能保持代码的美观，整洁和可读性。你可以在源文件夹中放若干张PNG图片，当LESS编译的时候，LESS文件只会引入需用到的PNG图片，不会引入不需要用到的PNG图片。
