---
title: Server-side usage
---

> Less can be used on the command line via npm, downloaded as a script file for the browser or used in a wide variety of third party tools. See the [Usage]({{rel 'usage'}}) section for more
detailed information.

---
标题：服务器端使用
---

> Less可以通过npm在命令行上使用，作为一个脚本文件浏览器或用于广泛的第三方工具下载。有关更多详细信息， 参见[Usage]({{rel 'usage'}}) 部分。

## Installation

The easiest way to install Less on the server, is via npm, the [node.js](http://nodejs.org/) package manager, as so:

## 安装

在[node.js](http://nodejs.org/)中安装LESS最简单的方式就是使用Node包管理工具npm来安装：*

在服务器上安装LESS最简单的方式就是使用[node.js]（http://nodejs.org/）包管理工具 npm 来安装：

```bash
$ npm install -g less
```

## Command-line usage

Once installed, you can invoke the compiler from the command-line, as such:

```bash
$ lessc styles.less
```

This will output the compiled CSS to `stdout`, you may then redirect it to a file of your choice:

```bash
$ lessc styles.less > styles.css
```

To output minified CSS, simply pass the `-x` option. If you would like more involved minification,
the [Clean CSS](https://github.com/GoalSmashers/clean-css) is also available with
the `--clean-css` option.

To see all the command line options run lessc without parameters.

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

## Usage in Code

You can invoke the compiler from node, as such:

```js
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, css) {
  console.log(css);
});
```

which will output

```css
.class {
  width: 2;
}
```

you may also manually invoke the parser and compiler:

```js
var parser = new(less.Parser);

parser.parse('.class { width: (1 + 1) }', function (err, tree) {
  if (err) {
    return console.error(err)
  }
  console.log(tree.toCSS());
});
```

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

## Configuration

You may pass some options to the compiler:

```js
var parser = new(less.Parser)({
  paths: ['.', './lib'], // Specify search paths for @import directives
  filename: 'style.less' // Specify a filename, for better error messages
});

parser.parse('.class { width: (1 + 1) }', function (e, tree) {
  tree.toCSS({
    // Minify CSS output
    compress: true
  });
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

Less also integrates with the popular build framework grunt, using the [grunt-contrib-less](https://github.com/gruntjs/grunt-contrib-less) plugin.

## Grunt

Less还集成了流行的构建框架grunt,使用[grunt-contrib-less](https://github.com/gruntjs/grunt-contrib-less)插件。

## Third party tools

See the [Usage]({{rel 'usage'}}) section for details of other tools.

# Client-side usage

> Using less.js in the browser is great for development, but it's not recommended for production

Client-side is the easiest way to get started and good for developing with Less, but in production, when performance and reliability is important, _we recommend pre-compiling using node.js or one of the many third party tools available_.

To start off, link your `.less` stylesheets with the `rel` attribute set to "`stylesheet/less`":

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

Next, [download less.js](https://github.com/less/less.js/archive/master.zip) and include it in a `<script></script>` tag in the `<head>` element of your page:

```html
<script src="less.js" type="text/javascript"></script>
```

## 第三方工具

有关其他工具详细信息,参见[Usage]({{rel 'usage'}}) 部分。

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

### Tips

* Make sure you include your stylesheets **before** the script.
* When you link more than one `.less` stylesheet each of them is compiled independently. So any variables, mixins or namespaces you define in a stylesheet are not accessible in any other.

### 特别注意

* 确保包涵`.less`样式表在`less.js`脚本**之前**
* 当你引入多个`.less`样式表时，它们都是独立编译的。所以，在每个文件中定义的变量、混合、命名空间都不会被其它的文件共享。

## Browser Options

Options are defined by setting them on a global `less` object **before** the `<script src="less.js"></script>`:

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
