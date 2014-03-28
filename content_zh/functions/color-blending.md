> 颜色混合的方式与图像编辑器 Photoshop, Firework 或者 GIMP 的图层混合模式 (layer blending modes) 相似，因此制作 .psd 文件时处理颜色的方法可以同样用在 CSS 中。


### multiply(@color1,@color2)

> 分别将两种颜色的红绿蓝 (RGB) 三种值做乘法运算，然后再除以255，输出结果是更深的颜色。（译注：对应Photoshop中的“变暗/正片叠底”。）

参数：

* `@color1`: 颜色对象( A color object)
* `@color2`: 颜色对象( A color object)

返回值: `颜色(color)`

**例如**:

```less
multiply(#ff6600, #000000);
```
![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
multiply(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#331400:#ffffff/text:331400)

```less
multiply(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
multiply(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#993d00:#ffffff/text:993d00)

```less
multiply(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
multiply(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
multiply(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
multiply(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
multiply(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)


### screen(@color1,@color2)

> 与`multiply()` 函数效果相反，输出结果是更亮的颜色。（译注：对应Photoshop中的“变亮/滤色”。）

参数：

* `@color1`: 颜色对象(A color object)
* `@color2`: 颜色对象(A color object)

返回值： `颜色(color)`

例如：

```less
screen(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
screen(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ffa366:#ffffff/text:ffa366)

```less
screen(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ffc299:#000000/text:ffc299)

```less
screen(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffe0cc:#000000/text:ffe0cc)

```less
screen(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
screen(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ffff00:#ffffff/text:ffff00)

```less
screen(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### overlay(@color1,@color2)

> 结合 `multiply()` 与 `screen()` 两个函数的效果，令浅的颜色变得更浅，深的颜色变得更深。（译注：对应Photoshop中的“叠加”。）**注意**：输出结果由第一个颜色参数决定。

参数：

* `@color1`: 颜色对象，是用于叠加的颜色，也是结果是更亮还是更暗的决定因素。
* `@color2`:  颜色对象，被_叠加_的颜色。

返回值： `颜色(color)`

例如：

```less
overlay(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
overlay(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5200:#ffffff/text:ff5200)

```less
overlay(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7a00:#ffffff/text:ff7a00)

```less
overlay(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffa300:#ffffff/text:ffa300)

```less
overlay(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)


### softlight(@color1,@color2)

> 与 `overlay()` 函数效果相似，只是当纯黑色或纯白色作为参数时输出结果不会是纯黑色或纯白色。（译注：对应Photoshop中的“柔光”。）

参数：

* `@color1`: 混合色（光源）
* `@color2`:  被混合的颜色

返回值： `颜色(color)`

例如：

```less
softlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff4100:#ffffff/text:ff4100)

```less
softlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5a00:#ffffff/text:ff5a00)

```less
softlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7200:#ffffff/text:ff7200)

```less
softlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ff8a00:#ffffff/text:ff8a00)

```less
softlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)


### hardlight(@color1,@color2)

> 与 `overlay()` 函数效果相似，不过由第二个颜色参数决定输出颜色的亮度或黑度，而不是第一个颜色参数决定。（译注：对应Photoshop中的“强光/亮光/线性光/点光”。）

参数：

* `@color1`: 混合色（光源）
* `@color2`: 颜色对象，用于叠加颜色，也是结果是更亮还是更暗的决定因素。

返回值： `颜色(color)`

例如：

```less
hardlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
hardlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
hardlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
hardlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
hardlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
hardlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
hardlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
hardlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#00ff00:#ffffff/text:00ff00)

```less
hardlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#0000ff:#ffffff/text:0000ff)


### difference(@color1,@color2)

> 从第一个颜色值中减去第二个（分别计算 RGB 三种颜色值），输出结果是更深的颜色。（译注：对应Photoshop中的“差值/排除”。）

参数：

* `@color1`: 被减的颜色对象
* `@color2`: 减去的颜色对象

返回值： `颜色(color)`

例如：

```less
difference(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
difference(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc3333:#ffffff/text:cc3333)

```less
difference(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#990066:#ffffff/text:990066)

```less
difference(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#663399:#ffffff/text:663399)

```less
difference(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#3366cc:#ffffff/text:3366cc)

```less
difference(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
difference(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
difference(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
difference(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### exclusion(@color1,@color2)

> 效果与 `difference()` 函数效果相似，只是输出结果差别更小 (lower contrast)。（译注：对应Photoshop中的“差值/排除”。）

参数：

* `@color1`: 被减的颜色对象
* `@color2`: 减去的颜色对象

返回值： `颜色(color)`

例如：

```less
exclusion(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
exclusion(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc7033:#ffffff/text:cc7033)

```less
exclusion(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#997a66:#ffffff/text:997a66)

```less
exclusion(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#668599:#ffffff/text:668599)

```less
exclusion(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#338fcc:#ffffff/text:338fcc)

```less
exclusion(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
exclusion(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
exclusion(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
exclusion(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### average(@color1,@color2)

> 分别对 RGB 的三种颜色值取平均值，然后输出结果。

参数：

* `@color1`: 颜色对象(A color object)
* `@color2`: 颜色对象(A color object)

返回值： `颜色(color)`

例如：

```less
average(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#803300:#ffffff/text:803300)

```less
average(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#994d1a:#ffffff/text:994d1a)

```less
average(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#b36633:#ffffff/text:b36633)

```less
average(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#cc804d:#ffffff/text:cc804d)

```less
average(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#e69966:#ffffff/text:e69966)

```less
average(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffb380:#000000/text:ffb380)

```less
average(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff3300:#ffffff/text:ff3300)

```less
average(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#80b300:#ffffff/text:80b300)

```less
average(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#803380:#ffffff/text:803380)

### negation(@color1,@color2)

> 与 difference() 函数效果相反，输出结果是更亮的颜色。请注意：效果相反不代表做加法运算。

参数：

* `@color1`: 被减的颜色对象
* `@color2`: 减去的颜色对象

返回值： `颜色(color)`

例如：

```less
negation(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
negation(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc9933:#ffffff/text:cc9933)

```less
negation(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#99cc66:#ffffff/text:99cc66)

```less
negation(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#66ff99:#ffffff/text:66ff99)

```less
negation(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#33cccc:#ffffff/text:33cccc)

```less
negation(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
negation(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
negation(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
negation(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#ffffff/text:ff66ff)
