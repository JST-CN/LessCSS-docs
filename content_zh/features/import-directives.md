> 从其他样式表中导入样式。

在标准的CSS中，`@import`必须在所有其他类型的规则之前。但是Less.js不在乎你把`@import`语句放在什么位置。

示例：

```less
.foo {
  background: #900;
}
@import "this-is-valid.less";
```

## 文件扩展名

`@import`语句会通过Less依赖文件扩展名的方式区别对待不同的文件：

* 如果文件有一个`.css`扩展名，则将它作为CSS对象，同时`@import`语句保持不变（查看下面的inline选项）
* 如果有_其他扩展名_，则作为Less对象，然后导入它。
* 如果没有扩展名，则插入`.less`，然后将它作为Less文件导入包含进来。

示例：

```less
@import "foo";      // foo.less is imported
@import "foo.less"; // foo.less is imported
@import "foo.php";  // foo.php imported as a less file
@import "foo.css";  // statement left in place, as-is
```
下面的选项可以用来重写这一行为。

# 导入选项

> Less提供了一系列的CSS扩展来让你使用`@import`更灵活的导入第三方CSS文件。

语法：`@import (keyword) "filename";`

下面导入指令已经被实现了：

* `reference`：使用Less文件但不输出
* `inline`：在输出中包含源文件但不加工它
* `less`：将文件作为Less文件对象，无论是什么文件扩展名
* `css`：将文件作为CSS文件对象，无论是什么文件扩展名
* `once`：只包含文件一次（默认行为）
* `multiple`：包含文件多次

## reference
> 使用`@import (reference)`导入外部文件，但是不添加导入的样式到编译输出中，只引用。

发布于 [v1.5.0]({{ less.master }}CHANGELOG.md)

示例： `@import (reference) "foo.less";`

`reference` 是Less语言中最强大的特性之一。想象以下，`reference`会使用一个_引用标记_在导入的文件中标记每个指令和选择器，正常导入它，但是生成CSS的时候，"引用的"选择器不会输出（和media query一样只包含选择器引用）。`reference`样式不会显示在生成的CSS中，除了应用作为mixin或者extend的样式。

此外，**`reference`**还依赖于使用的方法（mixin或者extend）生成不同的结果：

* **extend**：当一个选择是extended时，之后新的选择器会标记为_非引用_，然后将它插入引用`@import`语句的位置。
* **mixins**：当`reference`样式用作显示的mixin时，混合它的规则，标记为*非引用*，然后正常出现在引用它的地方。


### reference示例

这允许你通过做一些像下面这样的工作从诸如[Bootstrap](https://github.com/twbs/bootstrap)的库中拉入特定的，目标样式：

```less
.navbar:extend(.navbar all) {}
```

这样就只会从Bootstrap中拉入`.navbar`相关的样式。


## inline

> 使用`@import (inline)`引入外部文件，但不加工他们。

发布于 [v1.5.0]({{ less.master }}CHANGELOG.md)

示例: `@import (inline) "not-less-compatible.css";`

当一个CSS文件可能不兼容Less的时候可以使用这一技术，这是因为尽管Less支持大多数熟知的标准的CSS，但是在有些地方它还是不支持注释，在不修改CSS的情况下它也不支持所有已知的CSS hacks。

因此你可以使用它来在输出中引入文件，最终CSS文件都会在一个地方。

## less

> 使用`@import (less)`会将导入的文件作为Less文件对象，不管文件扩展名是什么。
> 
发布于 [v1.4.0]({{ less.master }}CHANGELOG.md)

示例：

```less
@import (less) "foo.css";
```


## css

> 使用`@import (css)`会将带入的文件作为普通的CSS文件对象，也不会管扩展名是什么。这意味着import语句把持不变。

发布于 [v1.4.0]({{ less.master }}CHANGELOG.md)

示例：

```less
@import (css) "foo.less";
```
输出：

```less
@import "foo.less";
```


## once

> `@import`语句的默认行为。这意味着文件只会被导入一次，而随后的导入文件的语句都会被忽略。

发布于 [v1.4.0]({{ less.master }}CHANGELOG.md)

这个`@import`语句的默认行为。

示例：

```less
@import (once) "foo.less";
@import (once) "foo.less"; // this statement will be ignored
```


## multiple

> 使用`@import (multiple)`允许导入多个同名文件。这与只能导入一次的行为是对立的。

发布于 [v1.4.0]({{ less.master }}CHANGELOG.md)

示例：

```less
// file: foo.less
.a {
  color: green;
}
// file: main.less
@import (multiple) "foo.less";
@import (multiple) "foo.less";
```
输出：

```less
.a {
  color: green;
}
.a {
  color: green;
}
```