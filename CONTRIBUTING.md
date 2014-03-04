## 贡献者指南

**格式规范**

为了使文档中所有示例保持一致并确保可读性，贡献文档时请遵循以下原则：

* 2个空格(Space)缩进，不使用制表符（Tab) ，始终保持缩进是正确的
* 使用多行书写属性的格式（每行一个属性和值）
* 对于多个用逗号分隔的选择器，每个选择器占一行
* 只使用双引号，不使用单引号
* 在属性的冒号后始终放置一个空格（例如， `display: block;` 而不是 `display:block;`）
* 所有行都要以分号结束
* 属性选择器中的属性值应该始终用双引号包裹，比如 `input[type="text"]` 。在你自己的代码中这样做也是对一致性和安全性很重要的。（见这篇博客 [提交 不带引号的属性值](http://mathiasbynens.be/notes/unquoted-attribute-values) 中的 XSS 攻击）
* 示例中使用HTML时，正确使用与HTML5 doctype对应的标签和元素的写法（例如，_自闭合标记_不写结束的斜杠）
* 所有页面的文件名应该全局唯一，不管这些文件在哪个文件夹中

## 工具

### Assemble

* 访问[Assemble的文档](http://assemble.io/docs/)学习更多关于定制和配置的知识。
* Markdown: [Markdown速查表](http://assemble.io/docs/Cheatsheet-Markdown.html)

## 代码风格

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

### 功能提议，Bug和Pull Request

* 如果你有功能提议，或者改进的建议，或者想报告一个bug，请[提交一个issue](https://github.com/JST-CN/lesscss.net/issues?state=open)。
* 提交功能提议时如果能包含一个描述清晰的使用案例，会更容易被重视。
* 如果你想提交一个Pull Request，请首先阅读[这个]({{ site.codebasemaster }}CONTRIBUTING.md)。
