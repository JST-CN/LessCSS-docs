---
标题： 开发 Less
---

感谢您考虑为此贡献。请先认真阅读[贡献说明]({{ less.master }}CONTRIBUTING.md)，以免造成浪费。

## 安装这些工具

* **node** - <http://nodejs.org/>
* **phantomjs** - <http://phantomjs.org/download.html>

确保环境变量（paths）已经配置好。 当你打开你最喜欢的命令行，执行 `node -v` 命令，你会看到node编译器版本号，执行 `phantomjs -v` 命令，你会看到phantomjs的版本号。

* 克隆你的 less.js 库到本地
* 前往你本地的 less.js 库然后执行 `npm install` 命令，这将会安装 less 的相关资源文件。
* 如果你之前没有用过grunt, 执行 `npm install grunt-cli -g`  命令，然后你就可以在各个地方（全局）执行“grunt”命令了。

## 使用

当你去到less库的根目录，你可以执行 `grunt test` 命令，这个操作将会执行所有的测试。 为特定的浏览器，执行 `grunt browsertest` 命令，如果你不想使用一个文件，而是想使用当前版本的less，请执行 `node bin/lessc path/to/file.less` 命令。

在浏览器调试，执行 `grunt browsertest-server` 命令，然后前往 http://localhost:8088/tmp/browser/ 去看测试运行的页面。

可选: 想要获得最新的 less 编译器，请执行 `npm -g install less` 命令， npm 是node的包管理， "-g" 表示安装之后全局有效。

现在你可以执行 `lessc file.less` 命令了，如果有一个相应的 file.less 文件，它将会被编译以及标准输出编译后的内容。 你可以拿它跟通过本地执行 (`node bin/lessc file.less`)后得到的文件进行对比下。

其他grunt命令

* `grunt benchmark` - 执行基准测试去获得一些性能指数
* `grunt stable` - 新建一个版本
* `grunt readme` - 在路径根目录新建一个 readme.md 文件（每产生一个新版本之后）

## 指南

你可以看看 [http://www.gliffy.com/go/publish/4784259](http://www.gliffy.com/go/publish/4784259)，  这是一个less工作原理概览图。


## Books

* [Less Web Development Essentials](http://www.packtpub.com/less-web-development-essentials/book), by Bass Jobsen, Foreword by Alexis Sellier
