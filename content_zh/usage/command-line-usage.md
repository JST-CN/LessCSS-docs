---
标题: 命令行使用
---

> 使用命令行编译 `.less` 文件生产 `.css`文件

<span class="warning">注意! 如果命令行不是你的长处, 更多的去了解 [GUIs for Less](#guis-for-less).</span>

### 安装Lessc到全局使用

用[npm](https://www.npmjs.org/)工具包安装

```bash
npm install less -g
```

然后你将可以使用 `lessc` 这个全局命令. 对于指定的版本(或者 标签) 你能在我们的安装包后添加 `@VERSION`, 例如. `npm install less@1.6.2 -g`.

### 安装到项目开发

另外如果你不使用全局编译器,你可能会

```bash
npm i less --save-dev
```

该命令会安装最新的lessc官方版本到你的项目文件夹, 同时会把它添加到你项目`package.json`文件的`devDependencies`.

请注意,[波浪线版本范围][]将自动在package.json中指定。这是对的,因为最新版本发布的新补丁将由npm安装。
#### lessc的测试版本

因为新功能将会定期的发布, lessc builds will be published to npm, tagged as. 这些版本_不会_作为`@latest`的正式发布,通常会带有个版本号或带`alpha/beta/release`字样的候选版本.

由于补丁发布是不间断的，我们会立即发布补丁版本和alpha/beta/候选版本将作为次要或主要版本升级（为了遵循[语义版本](http://semver.org/),我们会从1.4.0版本继续）。
Since patch releases are non-breaking we will publish patch releases immediately and alpha/beta/candidate versions will be published as minor or major version upgrades .

#### 安装lessc 未发布的开发版本

如果你想安装一个前沿,lessc未发布的版本,按照说明指定一个[git的URL作为一个依赖][]和一定要指定一个实际的提交SHA(不是一个分支的名字)使用`commit-ish`。这将保证您的项目总是使用lessc的具体版本.

指定的git URL 可能就是官方lessc的repo或者一个fork.


[tilde version range]: https://www.npmjs.org/doc/misc/semver.html#Ranges
[git URL as a dependency]: https://npmjs.org/doc/json.html#Git-URLs-as-Dependencies

### 服务器端命令行使用

这个资源库包含了二进制资源，`bin/lessc` 可以在安装有[Node.js](http://nodejs.org/) 的*nix, OSX and Windows这些平台上工作。
**Usage**: `lessc [option option=parameter ...] <source> [destination]`

### 命令行使用

```bash
lessc [option option=parameter ...] <source> [destination]
```

If source is set to `-' (dash or hyphen-minus), input is read from stdin.

#### 例如

```bash
# compile bootstrap.less to bootstrap.css
$ lessc bootstrap.less bootstrap.css

# compile bootstrap.less to bootstrap.css and minify (compress) the result
$ lessc -x bootstrap.less bootstrap.css
```

### 帮助

```bash
lessc --help
lessc --h
```

打印一个带有可选项的帮助菜单,然后退出

### Include paths

```bash
lessc --include-path=PATH1;PATH2
```

Sets available include paths. Separated by ':' or ';' on Windows.

Use this to configure a list of paths which less will use to find imports in. You might use this for instance to specify a path to a library which you want to be referenced simply and relatively in the less files.

In node, set a paths option
```js
{ paths: ['PATH1', 'PATH2']  }
```

### 生成文件

```bash
lessc -M
lessc --depends
```

### 不着色

```bash
lessc --no-color
```

### 不兼容IE

```bash
lessc --no-ie-compat
```

Currently only used for the data-uri function to ensure that images aren't created that are too large for the browser to handle.
目前仅用于 data-uri函数，确保创建出能够适合浏览器处理的图片大小。
### 禁用JavaScript

```bash
lessc --no-js
```

### Lint

```bash
lessc --lint
lessc --l
```

运行less转换器,仅仅会报告错误,无任何输出

### Silent

```bash
lessc -s
lessc --silent
```

### Strict Imports

```bash
lessc --strict-imports
```

### 允许导入不安全的https hosts

```bash
lessc --insecure
```

### 版本

```bash
lessc -v
lessc --version
```

### 压缩

```bash
lessc -x
lessc --compress
```

压缩使用less内置的压缩工具,这是一个好的习惯,但没有利用所有专用压缩css的技巧.您能发挥想象改进我们的压缩输出，通过提交pull request.

### 清理CSS

```bash
lessc --clean-css
```

清理CSS是我们minifer迷你化的选择,如果你想要最简化,请打开这个选项。

注意,它还不支持sourcemaps,要支持那样的话,你可以仅仅只使用我们的压缩。

### 带选项的CSS清理

```bash
lessc --clean-css --clean-option=--selectors-merge-mode:ie8 --clean-option=--advanced
```

使用这个命令传递选项清理，默认选项是最保险的清理，因为兼容IE8。

### 可输出自定义文件名的源代码映射(Source Map)

```bash
lessc --source-map
lessc --source-map=file.map
```

告诉less 生成一个源代码映射文件(sourcemap).如果不提供文件名映射，则使用源less编译后CSS全文件名来作为扩展映射名称。

### Source Map Rootpath源代码映射根路径

```bash
lessc --source-map-rootpath=dev-files/
```

Specifies a rootpath that should be prepended to each of the less file paths inside the sourcemap and also to the path to the map file specified in your output css.
指定一个根路径用于预设在源代码映射每一个less文件路径和编译生成的css文件中

Use this option if for instance you have a css file generated in the root on your web server but have your source less/css/map files in a different folder. So for the option above you might have
举例来说如果你有根生成的css文件在Web服务器上，但有你的源代码在不同的文件夹中少/ CSS/映射文件使用此选项。因此，对于你上面的选项可能有

```bash
output.css
dev-files/output.map
dev-files/main.less
```

### Source Map Basepath

```bash
lessc --source-map-basepath=less-files/
```

与根路径相反的相反的做法，它指明应当从输出路径被删除的路径。例如，如果你正在编译`less-files`目录的一个文件，但源文件将在根目录或当前目录下的Web服务器有效，您可以指定此项，移除输出路径中额外的``less-files``文件路径。
### Source Map Less Inline

```bash
lessc --source-map-less-inline
```

This option specifies that we should include all of the css files in to the sourcemap. This means that you only need your map file to get to your original source.
此选项指定所有的less文件原内容都会包括在源文件映射中，意味着获取你的.map文件就能获取less源代码.

This can be used in conjunction with the map inline option so that you do not need to have any additional external files at all.

### Source Map Map Inline

```bash
lessc --source-map-map-inline
```

This option specifies that the map file should be inline in the output CSS. This is not recommended for production, but for development it allows the compiler to produce a single output file which in browsers that support it, use the compiled css but show you the non-compiled less source.
此选项指定map文件应该内嵌在输出的CSS，在生产中不推荐，但对于开发环境，编译产生单个文件，使之浏览器支持显示编译的css而不是未编译的less资源
### Source Map URL

```bash
lessc --source-map-url=../my-map.json
```

Allows you to override the URL in the css that points at the map file. This is for cases when the rootpath and basepath options are not producing exactly what you need.
允许你重写你的，为了防止根路径和原路径选项没有正确生成你需要的情况。

### 根路径

```bash
lessc -rp=resources/
lessc --rootpath=resources/
```

允许你添加一个用于导入文件和Css文件生成的路径，这不会影响less 被编译的导入语句，仅仅影响停留在输出Css的位置。

例如，如果所有Css引用了resources文件的图片，你能使用此选项添加路径到URL，然后有你配置的文件夹名称。

### 相对路径

```bash
lessc -ru
lessc --relative-urls
```

默认情况下，URL是保持原样，因此当你导入一个引入了图片的子目录文件时，输出Css中路径也会相同。此选项允许您重写URL，将导入的文件的路径作为图片路径的相对路径，这样就确保URL总是相对于基于导入的文件。例如

```less
# main.less
@import "files/backgrounds.less";
# files/backgrounds.less
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

正常情况将输出如下：

```css
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

但是使用此选项则生成如下：

```css
.icon-1 {
  background-image: url('files/images/lamp-post.png');
}
```

你可能也想考虑使用能嵌入图片到css中的 data-uri函数替换这个选项。

### 严格的数学运算

```bash
lessc -sm=on
lessc --strict-math=on
```

默认关闭

如果这个选项关闭， Less将尝试计算你Css中所有的数学运算，例如.

```less
.class {
  height: calc(100% - 10px);
}
```

目前能被计算。

如果开启严格数学运算, 仅仅只有不必要的圆括号号内的运算会被计算，例如。

```less
.class {
  width: calc(100% - (10px  - 5px));
  height: (100px / 4px);
  font-size: 1 / 4;
}
```

```css
.class {
  width: calc(100% - 5px);
  height: 25px;
  font-size: 1 / 4;
}
```

我们原计划默认开启在将来,但它一直是contraversial选项,我们正在考虑是否用正确的方式解决了这个问题,或者是否Less应该有例外情况‘/’是有效的或Calc 是有用的
### 严格的单位

```bash
lessc -su=on
lessc --strict-units=on
```

默认关闭

没有这个选项, less 会尝试猜数学上单位输出。例如：

```less
.class {
  property: 1px * 2px;
}
```

对于这个例子，事情很明显不对，一个长度乘以另一个长度得到一个面积，但是css不支持这种面积，因此我们断定用户的意思是一个值乘以另外一个值，而不是长度单位，因此输出 `2px`.

如果这个选项开启，我们会断定是一个计算bug,然后报出一个错误。
### 全局变量

```bash
lessc --global-var="my-background=red"
```

这个选项定义一个能被文件引用的变量.高效的声明是放置在你基础Less文件的顶部,意味着他能被使用,但也能被覆盖如果在文件中定义了这个变量.

### 修改变量

```bash
lessc --modify-var="my-background=red"
```

与全局变量选项不同的是,这将在你的基础文件最后放置一个声明,意味着它将覆盖任何Less文件中的定义。

### URL 参数

```bash
lessc --url-args="cache726357"
```

这个选项允许你指定一个参数给每一个URL，这能破坏掉客户端缓存.
### 行号

```bash
lessc --line-numbers=comments
lessc --line-numbers=mediaquery
lessc --line-numbers=all
```

生成内联source-mapping. 这是浏览器开始支持sourcemaps之前唯一的选择。我们认为不以为然的,所以请联系如果你想要保留这个选项。
