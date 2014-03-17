### hue(@color)

> 从HSL色彩空间中提取颜色对象的色相值。

参数：`@color` - 颜色对象(a color object)

返回： `整数` `0-360`

例子： `hue(hsl(90, 100%, 50%))`

输出： `90`


### saturation(@color)

> 从HSL色彩空间中提取颜色对象的饱和度值。

参数： `@color` - 颜色对象(a color object)

返回： `百分比` `0-100`

例子： `saturation(hsl(90, 100%, 50%))`

输出： `100%`


### lightness(@color)

> 从HSL色彩空间中提取颜色对象的亮度值。

参数： `@color` - 颜色对象(a color object)

返回： `百分比` `0-100`

例子： `lightness(hsl(90, 100%, 50%))`

输出： `50%`


### hsvhue(@color)

> 从HSV色彩空间中提取颜色对象的色相值。

参数： `@color` - 颜色对象(a color object)

返回： `整数` `0-360`

例子： `hsvhue(hsv(90, 100%, 50%))`

输出： `90`


### hsvsaturation(@color)

> 从HSV色彩空间中提取颜色对象的饱和度值。

参数： `@color` - 颜色对象(a color object)

返回值： `百分比` 0-100

例子： `hsvsaturation(hsv(90, 100%, 50%))`

输出： `100%`


### hsvvalue(@color)

> 从色彩空间中提取颜色对象的色调值。

参数： `@color` - 颜色对象(a color object)

返回： `百分比` 0-100

例子： `hsvvalue(hsv(90, 100%, 50%))`

输出： `50%`


### red(@color)

> 提取颜色对象的红色值。

参数： `@color` - 颜色对象(a color object)

返回： `整数` `0-255`

例子： `red(rgb(10, 20, 30))`

输出： `10`


### green(@color)

> 提取颜色对象的绿色值。

参数： `@color` - 颜色对象(a color object)

返回： `整数` 0-255

例子： `green(rgb(10, 20, 30))`

输出： `20`


### blue(@color)

> 提取颜色对象的蓝色值。

参数： `@color` - 颜色对象(a color object)

返回： `整数` 0-255

例子： `blue(rgb(10, 20, 30))`

输出： `30`


### alpha(@color)

> 提取颜色对象的透明度值。

参数： `@color` - 颜色对象(a color object)

返回： `浮点数` `0-1`

例子： `alpha(rgba(10, 20, 30, 0.5))`

输出： `0.5`


### luma(@color)

> 计算颜色对象[luma](http://en.wikipedia.org/wiki/Luma_%28video%29)的值（亮度的百分比表示法）。

使用在WCAG2.0中定义的SMPTE C / Rec. 709 coefficients。 这个计算公式也用在 contrast() 函数中。

参数： `@color` - 颜色对象(a color object)

返回： `百分比` 0-100%

例子： `luma(rgb(100, 200, 30))`

输出： `65%`
