颜色值运算有几点注意事项：参数必须单位/格式相同；百分比将作为绝对值处理，比如 10% 增加 10%，结果是 20% 而不是 11%；参数值只能在限定的范围内；they do not wrap around (这一句不清楚意思，可能是指参数值不会在超过范围后自动从另一侧“穿越”回去。)。返回值时，除了十六进制的颜色值 (hex versions) 外将对其他格式做简化处理。

### saturate(@color,@amount)

> 增加一定数值的颜色饱和度。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `saturate(hsl(90, 80%, 50%), 20%)`

输出： `#80ff00 // hsl(90, 100%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80ff00:#000000/text:80ff00)

### desaturate(@color,@amount)

> 降低一定数值的颜色饱和度。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `desaturate(hsl(90, 80%, 50%), 20%)`

输出 `#80cc33 // hsl(90, 60%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80cc33:#000000/text:80cc33)

### lighten(@color,@amount)

> 增加一定数值的颜色亮度。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `lighten(hsl(90, 80%, 50%), 20%)`

输出： `#b3f075 // hsl(90, 80%, 70%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#b3f075:#000000/text:b3f075)

### darken(@color,@amount)

> 降低一定数值的颜色亮度。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `darken(hsl(90, 80%, 50%), 20%)`

输出： `#4d8a0f // hsl(90, 80%, 30%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#4d8a0f:#000000/text:4d8a0f)

### fadein(@color,@amount)

> 降低颜色的透明度（或增加不透明度），令其更不透明。

对不透明的颜色无效。如果要增加颜色的透明度，使用 `fadeout()` 函数。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `fadein(hsla(90, 90%, 50%, 0.5), 10%)`

输出： `rgba(128, 242, 13, 0.6) // hsla(90, 90%, 50%, 0.6)`


### fadeout(@color,@amount)

> 增加颜色的透明度（或降低不透明度），令其更透明。

对不透明的颜色无效。如果要增加颜色的透明度，使用`fadein()` 函数。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 0-100%

返回值： `颜色(color)`

例如： `fadeout(hsla(90, 90%, 50%, 0.5), 10%)`

输出： `rgba(128, 242, 13, 0.4) // hsla(90, 90%, 50%, 0.6)`


### fade(@color,@amount)

> 给颜色（包括不透明的颜色）设定一定数值的透明度。

参数：

* `@color`: 颜色对象(A color object)
* `@amount`: 百分比 范围：0-100%

返回值： `颜色(color)`

例如： `fade(hsl(90, 90%, 50%), 10%)`

输出： `rgba(128, 242, 13, 0.1) //hsla(90, 90%, 50%, 0.1)`


### spin(@color,@amount)

> 任意方向旋转颜色的色相角度 (hue angle)。

旋转范围 0-360，超过一周后将从起点开始继续旋转（+-控制方向），比如旋转360度与720度是相同的结果。需要注意的是，颜色值会通过RGB格式转换，这个过程不能保留灰色的色相值（灰色没有饱和度，色相值也就没有意义了），因此要确定使用函数的方法能够保留颜色的色相值，例如不要这样使用函数：

```less
@c: saturate(spin(#aaaaaa, 10), 10%);
```

而应该用这种方法代替：

```less
@c: spin(saturate(#aaaaaa, 10%), 10);
```

因为颜色值永远输出为 RGB 格式，因此 `spin()` 函数对灰色无效。

参数：

* `@color`: 颜色对象(A color object)
* `@angle`: 任意数字表示角度 （+ 或 – 表示方向）

返回值： `颜色(color)`

例如：

```less
spin(hsl(10, 90%, 50%), 30)
spin(hsl(10, 90%, 50%), -30)
```

输出：

```css
#f2a60d // hsl(40, 90%, 50%)
#f20d59 // hsl(340, 90%, 50%)
```

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f2a60d:#000000/text:f2a60d)

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f20d59:#000000/text:f20d59)

### mix(@color1,@color2, [@weight: 50%])

> 根据比例混合两种颜色，包括计算不透明度。

参数：

* `@color1`: 颜色对象(A color object)
* `@color2`: 颜色对象(A color object)
* `@weight`: 可选项：平衡两种颜色的百分比, 默认 50%。

返回值： `颜色(color)`

例如：

```less
mix(#ff0000, #0000ff, 50%)
mix(rgba(100,0,0,1.0), rgba(0,100,0,0.5), 50%)
```

输出：

```css
#800080
rgba(75, 25, 0, 0.75)
```

![Color 1](holder.js/100x40/#ff0000:#ffffff/text:ff0000) + ![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff) ➜ ![Color 3](holder.js/100x40/#800080:#ffffff/text:800080)

### greyscale(@color)

> 完全移除颜色的饱和度，与 `desaturate(@color, 100%)` 函数效果相同。

因为颜色的饱和度不受色相值影响，所以输出的颜色会稍显暗淡 (dull or muddy)；如果使用[`luma`](#color-channel-luma)值可能会有更好的结果，因为它提取的是百分比亮度，而不是线性亮度。比如`greyscale('#0000ff')`与`greyscale('#00ff00')`会得出相同的结果，尽管对人眼来说，它们的亮度是不一样的。

参数： `@color`: 颜色对象(A color object)

返回值： `颜色(color)`

例如： `greyscale(hsl(90, 90%, 50%))`

输出： `#808080 // hsl(90, 0%, 50%)`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#808080:#000000/text:808080)

注意：即便它们的亮度值(lightness value)一样，但是生成的灰色看起来比原来的绿色更暗些。

与`luma`相比较(因为`luma`返回一个单独的值，而不是颜色，所以它们的用法不一样)：

```less
@c: luma(hsl(90, 90%, 50%));
color: rgb(@c, @c, @c);
```

输出： `#cacaca`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#cacaca:#000000/text:cacaca)

实际上灰色的值跟高些，但是灰色的亮度值跟绿色的看起来大致上相同。

### contrast(@background, [@darkcolor: black], [@lightcolor: white], [@threshold: 43%])

> 选择两种颜色相比较，得出哪种颜色的对比度最大就倾向于对比度最大的颜色。


这个函数对比 @background 的 luma 值与 @threshold 参数的大小，如果大于输出 @darkcolor, 小于则输出 @lightcolor，便于选择相对于背景更容易阅读的颜色，同时提高了使用颜色的灵活性，与 [Compass 的 contrast() 函数](http://compass-style.org/reference/compass/utilities/color/contrast/) 工作方式相同。根据 [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef) 应该对比颜色的 luma 值，而不是亮度值 (lightness)。


`@light` 和 `@dark` 两个参数可以调换顺序。因为`contrast()`函数会自动计算它们的luma值和自动分配`@light`和`@dark`，这样你就不用通过颠倒两个参数的顺序才能选到最小对比度颜色(the *least* contrasting color)。

参数：

* `@color`: 需要对比的颜色对象 (A color object to compare against.)
* `@dark`: 可选项 – 指定的黑色（默认 black）
* `@light`: 可选项 – 指定的白色（默认 white）
* `@threshold`: 可选项 – 百分比 0-100% 界定深色过渡到浅色的转变位置（默认 43%），这个数值决定了输出结果偏向于哪一方，比如判断 50% 的灰色背景应该显示白色还是黑色的文字。一般来说，如果本色方案偏浅，则应该设低一点，否则设高一点。

返回值： `颜色(color)`

例如：

```less
contrast(#aaaaaa)
contrast(#222222, #101010)
contrast(#222222, #101010, #dddddd)
contrast(hsl(90, 100%, 50%), #000000, #ffffff, 40%);
contrast(hsl(90, 100%, 50%), #000000, #ffffff, 60%);
```

输出：

```
#000000 // 黑色
#ffffff // 白色
#dddddd
#000000 // 黑色
#ffffff // 白色
```

这些例子是利用计算颜色的值作为背景色和前景色。正如你所见，即便可能使用阈值允许得出更低对比度的颜色，但是不可能白衬白结束，也不可能黑衬黑结束。如最后一个例子：

![Color 1](holder.js/100x40/#aaaaaa:#000000/text:000000)
![Color 1](holder.js/100x40/#222222:#ffffff/text:ffffff)
![Color 1](holder.js/100x40/#222222:#dddddd/text:dddddd)
![Color 1](holder.js/100x40/#80ff00:#000000/text:000000)
![Color 1](holder.js/100x40/#80ff00:#ffffff/text:ffffff)
