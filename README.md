[![devDependency Status](https://david-dm.org/less/less-docs/dev-status.png)](https://david-dm.org/less/less-docs#info=devDependencies)

# lesscss.net

> Less/Less.js 中文官方站点和文档 

## 快速入门


文档使用 [Assemble](http://assemble.io) 和 [Grunt](http://gruntjs.com)工具 .按如下步骤准备:

1. 下载该项目文档
2. 在该项目的根目录下，键入命令 `npm install`
3. 再次键入命令 `grunt` 构建文档

如果一切工作正常，你可以开始贡献文档了！

### 文档

所有文档结构能在 `./content` 目录找到。如果你想添加文档，请阅读 **贡献** 以下部分。

## 计划

1. 清理和归整 [content](./content) 目录下的所有文档,意味着
2. 文件统一的命名规范，文档中统一的代码风格
3. 组织信息和支持单个文件的部分内容,而不是长文档
4. 最后，一个新的主题




## 贡献
### 编码风格
> 协助贡献时，请遵循如下指导方针以确保文档一致性，可读性，可维护性：

#### Markdown 标准

* 标题使用 `#`，不是下划线。下划线没有语义，不灵活，不总是正确高亮在代码标记器
* 在 `#` 和 标题 之间保留一个空格
* 使用**单撇号**包裹 内联代码
* 使用**三撇号**包括 代码块
* 在代码块中，第一个三引号后_总是使用正确的语言_。虽然GitHub上并不突出Less，当使用正确的语言时，我们的文档更容易在GitHub上的和谷歌的搜索结果中显示出来。例如：请用<code>\`\`\`less</code> 针对less，和 <code>\`\`\`css</code> 针对 CSS.


#### Less 标准

* 2个空格(Space)缩进, 绝对没有制表符（Tab) 一直采取适当的缩进
* 多行（Multiple-line）格式化(每行一个属性和值)
* 对于多个，用逗号分隔的选择，将每个选择在自己的行
* 仅有双引号,绝无单引号
* 在属性的冒号后始终放置一个空格(Space) (例如， `display: block;` 而不是 `display:block;`)
* 所有行结尾使用一个分号
* 属性选择器, 像 `input[type="text"]` 应该一直使用双引号包括属性的值.这是非常重要的做法在你自己的代码里此外也是为了一致性和安全(见这篇博客 [提交 不带引号的属性值](http://mathiasbynens.be/notes/unquoted-attribute-values) 导致的 XSS 攻击)
* 当你的例子使用了HTML，比如对于HTML5 doctype类型，使用正确的标签和元素的doctype（例如，_无结尾标签_的自结束标签的元素)

示例:

**优雅的写法**

```css
body {
  padding-top: 80px;
  font-size: 12px;
}
```

**不雅的写法**

```css
body {
padding-top: 80px;
font-size: 12px;
}
```

**不雅的写法**

```css
body { padding-top: 80px; font-size: 12px }
```

同时，请确保所有文档文件应该有一个全局唯一名称，不管他们位于哪个存储库，这会更易于使用在方便文件匹配，也是一个好的实践。

### 功能提议，Bugs和Pull请求

* 如果你有功能提议，或者改进的建议，或者报告一个bug，请[提交一个议题 ](https://github.com/less/less.js/issues?state=open).
* 如果你包含了一个清晰描述的使用案例，功能提议可能更容易被重视.
* 如果你想提交一个Pull请求, 请 [首先阅读](https://github.com/less/less.js/blob/master/CONTRIBUTING).md.

## 工具

文档站点是使用 [Assemble](http://assemble.io) 工具. 请访问这个项目 [报告bugs ](https://github.com/assemble/assemble/issues?state=open), 或者了解更多关于使用和定制的知识.

## 建立文档

从Less.js项目获取最新的元数据更新项目,如当前的版本号,描述,等等,然后用以下命令运行 Grunt :

```bash
node data/utils/pkg && grunt
```

## 许可证
Copyright (c) 2014, Alexis Sellier, LESS Core Team, Contributors
文档发布于 [Creative Commons](./LICENSE-CC).
文档源代码发布于 [MIT License](./LICENSE-MIT).
Less.js 源代码发布于 [Apache 2 License](https://github.com/less/less.js/blob/master/LICENSE).
