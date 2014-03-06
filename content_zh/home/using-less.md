---
标题：服务器端使用
---

> Less可以通过npm在命令行上使用，作为一个脚本文件浏览器或用于广泛的第三方工具下载。有关更多详细信息， 参见[用法]({{rel 'usage'}}) 部分。

## 安装

在[node.js](http://nodejs.org/)中安装LESS最简单的方式就是使用Node包管理工具npm来安装：*

在服务器上安装LESS最简单的方式就是使用[node.js](http://nodejs.org/)包管理工具 npm 来安装：

```bash
$ npm install -g less
```

## 在命令行中使用

一旦安装完成，就可以在命令行中调用，例如：

```bash
$ lessc styles.less
```

这样的话编译后的CSS将会输出到stdout中，你可以选择将这个输出重定向到文件中：

```bash
$ lessc styles.less > styles.css
```

如果你想输出一个压缩后的CSS，只要加到‘-x’选项即可。如果你想要更NB的压缩，你也可以选择使用[Clean CSS](https://github.com/GoalSmashers/clean-css)压缩器，只要加上"--clean-css"选项即可。

直接运行lessc，不带任何参数将可以看到所有的命令行参数。

## 在Node.js代码中使用 

你可以在Node中调用编译器，例如：

```js
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, css) {
  console.log(css);
});
```

将会输出

```css
.class {
  width: 2;
}
```

你也可以手工调用解析器和编译器：

```js
var parser = new(less.Parser);

parser.parse('.class { width: (1 + 1) }', function (err, tree) {
  if (err) {
    return console.error(err)
  }
  console.log(tree.toCSS());
});
```

## 设置

你可以给编译器传入一些参数：

```js
var parser = new(less.Parser)({
  paths: ['.', './lib'], // 指定@import搜索的目录
  filename: 'style.less' // 为了更好地输出错误信息，可以指定一个文件名
});

parser.parse('.class { width: (1 + 1) }', function (e, tree) {
  tree.toCSS({
    // 压缩输出的CSS
    compress: true
  });
});
```

## Grunt

Less还集成了流行的构建框架grunt,使用[grunt-contrib-less](https://github.com/gruntjs/grunt-contrib-less)插件。

## 第三方工具

有关其他工具详细信息,参见[用法]({{rel 'usage'}}) 部分。

# 在浏览器中使用LESSCSS

> 在浏览器中使用less.js开发是很好的，但不推荐用于生产环境中。*

浏览器端使用是在使用LESS开发时最直观的一种方式。如果是在生产环境中，尤其是对性能要求比较高的场合，_建议使用node或者其它第三方工具先编译成CSS再上线使用_。

首先，引入`rel`属性的值是`stylesheet/less`的`.less`样式表。

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

接下来，[下载 less.js](https://github.com/less/less.js/archive/master.zip)并将其包涵在您的页面`<head>`元素的`<script></script>`标记中：

```html
<script src="less.js" type="text/javascript"></script>
```

### 特别注意

* 确保包涵`.less`样式表在`less.js`脚本**之前**
* 当你引入多个`.less`样式表时，它们都是独立编译的。所以，在每个文件中定义的变量、混合、命名空间都不会被其它的文件共享。

## 浏览器选项

你可以引入`<script src="less.js"></script>`**之前**通过创建一个全局`less`对象的方式来指定参数，例如：

``` html
<!-- set options before less.js script -->
<script>
  less = {
    env: "development",
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```
