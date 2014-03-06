### escape 转义函数

> Applies [URL-encoding](http://en.wikipedia.org/wiki/Percent-encoding) to special characters found in the input string.

* 不转义编码的字符: `,`, `/`, `?`, `@`, `&`, `+`, `'`, `~`, `!` and `$`.
* 最常见的转义编码字符: `\<space\>`, `#`, `^`, `(`, `)`, `{`, `}`, `|`, `:`, `>`, `<`, `;`, `]`, `[` and `=`.

参数: `string`: 需要转义的字符串

返回: 不带引号的转义字符串。

例如:

```less
escape('a=1')
```

输出:

```css
a%3D1
```

注意: 如果一个参数不是一个字符串, 输出是未定义.当前的实现是颜色返回`undefined`，其他种类参数原样输出，这种转义不可靠，将来也许会改变。

### e 预判函数

> Css 转义, 用`~"值"` 符号代替。


他认为字符串是一个参数返回不带引号的原内容。这可以用来输出一些Less并不认可的Css值，包括未验证的Css语法或者一个专有的语法。

参数: `string` - 用来转义的字符串.

返回: `string` - 不带引号的转义字符串。

例如:

```less
filter: e("ms:alwaysHasItsOwnSyntax.For.Stuff()");
```

输出:

```css
filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
```

注意: 该函数也接受 `~""` 转义值和数字做参数，其他类型参数会返回一个错误。 


### % 百分号格式化参数

> 函数 `%(string, arguments ...)` 格式化一个字符串.

第一个参数是带占位符的字符串. 所有占位符始于百分号`%`后跟字母`s`,`S`,`d`,`D`,`a`, or `A`. 剩下的参数是替换占位符的表达式. 如果你需要输出百分号, 用双百分号转义`%%`.

如果你需要把特殊字符转义成 utf-8转义码请使用大写字母占位符，该占位符会转义所有的特殊字符除了`()'~!`。空格会被转义成`%20`。小写字母占位符会保留特殊字符的原样。

占位符:
* `d`, `D`, `a`, `A` - 能被任何类型参数替换 (颜色值, 数字, 转义值, 表达式, ...). 如果你在字符串中结合使用, 整个字符串参数都会替换进去 - 包括它的引号. 然后, 然后引号会被替换到字符串参数的原有位置, 也许会被转义或者还是不变的，取决于占位符是大写字母还是小写字母。
* `s`, `S` - 能被除了颜色值以为任何类型参数替换. 如果你在字符串中结合使用, 只会替换成字符串参数的值，-而字符串参数引号都被忽略

参数:

* `string`: 带占位符的格式化字符串,
* `anything`* : 替换占位符的值.

返回: 格式化后的字符串 `string`.

例如:

```less
format-a-d: %("repetitions: %a file: %d", 1 + 2, "directory/file.less");
format-a-d-upper: %('repetitions: %A file: %D', 1 + 2, "directory/file.less");
format-s: %("repetitions: %s file: %s", 1 + 2, "directory/file.less");
format-s-upper: %('repetitions: %S file: %S', 1 + 2, "directory/file.less");
```
输出:

```css
format-a-d: "repetitions: 3 file: "directory/file.less"";
format-a-d-upper: "repetitions: 3 file: %22directory%2Ffile.less%22";
format-s: "repetitions: 3 file: directory/file.less";
format-s-upper: "repetitions: 3 file: directory%2Ffile.less";
```


### replace 替换

> 用另一个字符串替换文本.

发布于 [v1.7.0]({{ less.master }}CHANGELOG.md)

参数:

* `string`: 搜索和替换用的字符串.
* `pattern`:一个字符串或者能搜索的正则表达式.
* `replacement`: 匹配模式成功的替换字符串.
* `flags`: (可选的) 正则表达式匹配标识（全匹配还是...）.

返回: 替换过值后的字符串.

例如:

```less
replace("Hello, Mars?", "Mars\?", "Earth!");
replace("One + one = 4", "one", "2", "gi");
replace('This is a string.', "(string)\.$", "new $1.");
replace(~"bar-1", '1', '2');
```
结果:

```css
"Hello, Earth!";
"2 + 2 = 4";
'This is a new string.';
bar-2;
```
