# lesscss.net

> Less/Less.js 中文官方网站 

## 快速入门

本文档使用 [Assemble](http://assemble.io) 和 [Grunt](http://gruntjs.com) 构建。构建步骤如下:

1. 下载本项目文档
2. 在本项目的根目录下，执行 `npm install`
3. 执行 `grunt` 命令构建文档

如果一切顺利的话，就可以开始贡献文档了！

### 文档

所有文档内容都存放在 `./content` 目录，如果你想添加文档，请先阅读下方的 **文档规范** 部分。

## 计划

1. 清理和归整 [content](./content) 目录下的所有文档，需要做的事情有
2. 统一的文件命名规范，统一的文档代码风格
3. 组织信息，尽量将内容的各部分拆为单个文件，而不是长文档
4. 最后，一套新的皮肤

## 文档规范

### 编码风格

> 在本项目中贡献文档时，请遵循如下指导方针以确保文档的一致性、可读性和可维护性：

#### Markdown 规范

* 标题使用 `#` 而不是下划线。因为下划线没有语义，也不灵活，而且在代码高亮时并不总是很准确
* 在 `#` 和标题之间保留一个空格
* 使用**单撇号**包裹内联代码
* 使用**三撇号**包括代码块
* 在代码块开始标记后面，紧跟正确的语言。虽然GitHub并不高亮Less代码，但当使用正确的语言时，我们的文档更容易在GitHub和谷歌的搜索结果中显示出来。例如：Less代码请使用<code>\`\`\`less</code>，CSS代码请使用<code>\`\`\`css</code>。


#### Less 规范

* 2个空格(Space)缩进, 不使用制表符（Tab) ，始终保持缩进是正确的
* 使用多行（Multiple-line）书写属性的格式（每行一个属性和值）
* 对于多个用逗号分隔的选择器，每个选择器占一行
* 只使用双引号，不使用单引号
* 在属性的冒号后始终放置一个空格（例如， `display: block;` 而不是 `display:block;`）
* 所有行尾都使用一个分号
* 属性选择器中的属性值应该始终用双引号包裹，比如 `input[type="text"]` 。在你自己的代码中这样做也是对一致性和安全性很重要的。（见这篇博客 [提交 不带引号的属性值](http://mathiasbynens.be/notes/unquoted-attribute-values) 中的 XSS 攻击）
* 示例中使用HTML时，正确使用与HTML5 doctype对应的标签和元素的写法（例如，_自闭合标记_不写结束的斜杠）

示例:

**好的写法**

```css
body {
  padding-top: 80px;
  font-size: 12px;
}
```

**不好的写法**

```css
body {
padding-top: 80px;
font-size: 12px;
}
```

**不好的写法**

```css
body { padding-top: 80px; font-size: 12px }
```

同时，请确保所有文档文件名是全局唯一的，而不管他们位于哪个目录，这会使得文件匹配更容易，这也是一个好的实践方式。

### 功能提议，Bug和Pull Request

* 如果你有功能提议，或者改进的建议，或者报告一个bug，请[提交一个issue](https://github.com/JST-CN/lesscss.net/issues?state=open).
* 提交功能提议时如果能包含一个描述清晰的使用案例，会更容易被重视.
* 如果你想提交一个Pull Request, 请 [首先阅读这个](https://github.com/JST-CN/lesscss.net/blob/master/CONTRIBUTING).md。

## 工具

本文档站点使用 [Assemble](http://assemble.io) 工具构建。如有需要，请访问这个项目 [报告bugs ](https://github.com/assemble/assemble/issues?state=open)，或者自行了解更多关于使用和定制的知识。

## 构建文档

首先从Less.js项目获取最新的元数据，如当前的版本号、描述等等，然后更新本项目，再使用以下命令运行 Grunt :

```bash
node data/utils/pkg && grunt
```

## 许可证
Copyright (c) 2014, Alexis Sellier, LESS Core Team, Contributors
文档使用 [Creative Commons](./LICENSE-CC) 协议发布。
文档源代码使用 [MIT License](./LICENSE-MIT) 协议发布。
Less.js 源代码使用 [Apache 2 License](https://github.com/less/less.js/blob/master/LICENSE) 协议发布。
