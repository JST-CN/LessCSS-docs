## 贡献文档

**格式规范**

为了文档中所有实例的一致性及确保我们代码示例的可读性，贡献时请遵循以下原则：

* 合理的使用缩进，缩进格式为四个空格
* 多行格式( 每行一个属性和对应的值 )
* 请使用双引号，避免出现单引号
* 在属性值冒号后面使用一个空格符( 例: `display: block;` 而不是 `display:block;` ) 
* 每行请以分号结束
* 对于多个用逗号分割的选择器，将每个选择器独立分为一行
* 属性选择器, 例：`input[type="text"]` 应将属性值放在双引号之间. 这对确保您的代码一致性和安全性非常重要( 请参见 [blog post on unquoted attribute values](http://mathiasbynens.be/notes/unquoted-attribute-values)，可能导致 XSS 攻击 )
* 当您的例子中有使用 HTML 时，请使用符合 HTML5 Doctype 的标签和元素( 例：自结束标签没有结尾的斜线 )
* 所有的页面文件的名称应保持在整个库中的唯一性

## 工具

### Assemble

* Visit [Assemble's documentation](http://assemble.io/docs/) site to learn more about customization and configuration.
* Markdown: [Markdown Cheatsheet](http://assemble.io/docs/Cheatsheet-Markdown.html)

## 代码风格

示例:

**正确的**

```css
body {
  padding-top: 80px;
  font-size: 12px;
}
```

**错误的**

```css
body {
padding-top: 80px;
font-size: 12px;
}
```

**错误的**

```css
body { padding-top: 80px; font-size: 12px }
```

### 功能需求, Bugs 提交及 Pull Requests

* 如果你有新的功能需求、提出改进或报告BUG，请 [提交一个 Issue]({{ site.codeissues }}).
* 功能需求请提供一个清楚的描述用例，以便更容易被重视.
* 如果您想要提交 pull request，请[首先阅读此文档]({{ site.codebasemaster }}CONTRIBUTING).md
