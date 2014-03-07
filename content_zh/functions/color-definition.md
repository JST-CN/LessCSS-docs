### rgb

> 创建一个十进制值分别为red，green和blue（RGB）的不透明的颜色对象。

在规范的HTML/CSS格式中，颜色字面量也被用于定义颜色，例如“#ff0000”。

参数：
* `red`: An integer 0-255 or percentage 0-100%.
* `green`: An integer 0-255 or percentage 0-100%.
* `blue`: An integer 0-255 or percentage 0-100%.

返回： `color`

例子： `rgb(90, 129, 32)`

输出： `#5a8120`


### rgba

> 创建一个十进制值分别为red,green,blue和alpha(透明度)（RGBA）的透明颜色对象。

参数：

* `red`: An integer 0-255 or percentage 0-100%.
* `green`: An integer 0-255 or percentage 0-100%.
* `blue`: An integer 0-255 or percentage 0-100%.
* `alpha`: A number 0-1 or percentage 0-100%.

返回： `color`

例子： `rgba(90, 129, 32, 0.5)`

输出： `rgba(90, 129, 32, 0.5)`


### argb

> 创建一个十六进制颜色表达式，以#RRGGBBAA格式为(**NOT** `#RRGGBBAA`!)。

这种格式被用于Internet Explorer，.NET和Android开发。

参数： `color`, color object.

返回： `string`

例子： `argb(rgba(90, 23, 148, 0.5));`

输出： `#805a1794`


### hsl

> 创建一个值分别为hue（色相），saturation（饱和度） 和 lightness(亮度) (HSL)的不透明的颜色对象。

参数：

* `hue`: An integer 0-360 representing degrees.
* `saturation`: A percentage 0-100% or number 0-1.
* `lightness`: A percentage 0-100% or number 0-1.

返回：`color`

例子：`hsl(90, 100%, 50%)`

输出：`#80ff00`

如果你想创建一个新的颜色是基于其他的色相，hsl是非常有用的，例如：“@new: hsl(hue(@old), 45%, 90%);”

@new和@old色相(hue)一致，饱和度(saturation)和亮度(lightness)是刚刚设定的新值


### hsla

> 创建一个值分别为hue（色相），saturation（饱和度），lightness(亮度)和alpha(透明度) (HSLA)透明的颜色对象。

Parameters:
参数：

* `hue`: An integer 0-360 representing degrees.
* `saturation`: A percentage 0-100% or number 0-1.
* `lightness`: A percentage 0-100% or number 0-1.
* `alpha`: A percentage 0-100% or number 0-1.

返回： `color`

例子： `hsl(90, 100%, 50%, 0.5)`

输出： `rgba(128, 255, 0, 0.5)`

### hsv

> 创建一个值分别为hue（色相），saturation（饱和度）和value（值）（HSV）不透明的颜色对象。

注意：这是在Photoshop中可用的色彩空间，和“hsl”是不一样。

参数：
* `hue`: An integer 0-360 representing degrees.
* `saturation`: A percentage 0-100% or number 0-1.
* `value`: A percentage 0-100% or number 0-1.

返回： `color`

例子： `hsv(90, 100%, 50%)`

输出： `#408000`


### hsva

> 创建一个值分别为hue（色相），saturation（饱和度），value（值）和alpha（透明度）（HSVA）透明的颜色对象。

注意：这是在Photoshop中可用的色彩空间，和“hsla”不一样。

参数：
* `hue`: An integer 0-360 representing degrees.
* `saturation`: A percentage 0-100% or number 0-1.
* `value`: A percentage 0-100% or number 0-1.
* `alpha`: A percentage 0-100% or number 0-1.

返回： `color`

例子： `hsva(90, 100%, 50%, 0.5)`

输出： `rgba(64, 128, 0, 0.5)`
