### rgb(@red,@green,@blue)

> 通过十进制红色，绿色，蓝色三种值 (RGB) 创建不透明的颜色对象。

在 HTML/CSS 中也会用文本颜色值 (literal color values) 定义颜色，例如 red -> #ff0000

参数：
* `@red`: 整数 0-255 或百分比 0-100%
* `@green`: 整数 0-255 或百分比 0-100%
* `@blue`: 整数 0-255 或百分比 0-100%

返回值： `颜色(color)`

例如： `rgb(90, 129, 32)`

输出： `#5a8120`


### rgba(@red,@green,@blue,@alpha)

> 通过十进制红色，绿色，蓝色，以及 alpha 四种值 (RGBA) 创建带alpha透明的颜色对象。

参数：

* `@red`: 整数 0-255 或百分比 0-100%.
* `@green`: 整数 0-255 或百分比 0-100%.
* `@blue`: 整数 0-255 或百分比 0-100%.
* `@alpha`: 数字 0-1 或百分比 0-100%.

返回值： `颜色（color）`

例如： `rgba(90, 129, 32, 0.5)`

输出： `rgba(90, 129, 32, 0.5)`


### argb(@color)

> 创建格式为 `#AARRGGBB` 的十六进制 (hex representation) 颜色 (注意不是 #RRGGBBAA ！)。

这种格式被用在IE滤镜中，以及.NET和Android开发中。

参数： `@color`: 颜色对象（color object）

返回值： `字符串(string)`

例如： `argb(rgba(90, 23, 148, 0.5));`

输出： `#805a1794`


### hsl（@hue,@saturation,@lightness）

> 通过色相 (hue)，饱和度 (saturation)，亮度 (lightness) 三种值 (HSL) 创建不透明的颜色对象。

参数：

* `@hue`: 整数 0-360 表示度数
* `@saturation`: 整数 0-100% 或是数字 0-1
* `@lightness`: 整数 0-100% 或是数字 0-1

返回值：`颜色（color）`

例如：`hsl(90, 100%, 50%)`

输出：`#80ff00`

当你想使用一种颜色来创建另一种颜色时很方便，如：`@new: hsl(hue(@old), 45%, 90%);`

`@new` 将使用 `@old` 的 *色相值*(hue)，以及它自己的饱和度与亮度。


### hsla（@hue,@saturation,@lightness,@alpha）

> 通过色相 (hue)，饱和度 (saturation)，亮度 (lightness)，以及 alpha 四种值 (HSLA) 创建透明的颜色对象。

参数：

* `@hue`: 整数 0-360 表示度数
* `@saturation`: 百分比 0-100% 或数字 0-1.
* `@lightness`: 百分比 0-100% 或数字 0-1.
* `@alpha`: 百分比 0-100% 或数字 0-1.

返回值： `颜色（color）`

例如： `hsl(90, 100%, 50%, 0.5)`

输出： `rgba(128, 255, 0, 0.5)`

### hsv(@hue,@saturation,@value)

> 通过色相 (hue)，饱和度 (saturation)，色调 (value) 三种值 (HSV) 创建不透明的颜色对象。

注意: HSV 与 HSL 不同，HSV是另一种在Photoshop中可用的色彩空间

参数：
* `@hue`: 整数 0-360 代表度数
* `@saturation`: 百分比 0-100% 或数字 0-1
* `@value`: 百分比 0-100% 或数字 0-1

返回值： `颜色（color）`

例如： `hsv(90, 100%, 50%)`

输出： `#408000`


### hsva（@hue,@saturation,@value,@alpha）

> 通过色相 (hue)，饱和度 (saturation)，色调 (value)，以及 alpha 四种值 (HSVA) 创建透明的颜色对象。

注意：`HSVA` 与 `HSLA` 不同，`HSVA`另一种在Photoshop中可用的色彩空间。

参数：
* `@hue`: 整数 0-360 代表度数
* `@saturation`: 百分比 0-100% 或数字 0-1
* `@value`: 百分比 0-100% 或数字 0-1
* `@alpha`: 百分比 0-100% 或数字 0-1

返回值： `颜色（color）`

例如： `hsva(90, 100%, 50%, 0.5)`

输出： `rgba(64, 128, 0, 0.5)`
