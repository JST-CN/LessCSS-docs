---
title: 在浏览器中使用LESSCSS
---

### 监视模式
为了能够启用监视模式，env必须要设置成development。然后在引入的less.js文件之后调用less.watch(),例如：

```html
<script src="less.js"></script>
<script>less.watch();</script>
```

另外，你也可以在URL中加入#!watch来临时开启监视模式。

### 修改变量
使用modifyVars可以在运行时修改LESS变量。当用新的变量调用了这个函数时，LESS文件将被重新编译，但是不会被重新加载。一个基本的用法示例：

```js
less.modifyVars({
  '@buttonFace': '#5B83AD',
  '@buttonText': '#D9EEF2'
});
```

### 调试
我们在生成的CSS中带上额外的信息，以便一些调试工具可以定位到LESS文件中的行数。

可以通过dumpLineNumbers选项或者在URL中添加!dumpLineNumbers:mediaQuery来开启这个功能。

你可以选择“注释”方式，使用[FireLESS](https://addons.mozilla.org/en-us/firefox/addon/fireless/)来调，或者选择“mediaQuery”方式，使用FireBug/Chrome开发者工具（被识别为SCSS media query调试格式）来调试。

## 客户端的用法

你可以引入less.js之前通过创建一个全局less对象的方式来指定参数，例如：

``` html
<!-- 在less.js之前设置对象 -->
<script>
  less = {
    env: "development",
    logLevel: 2,
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    globalVars: {
      var1: '"string value"',
      var2: 'regular value'
    },
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```

### less对象参数说明

#### async
类型： `布尔值（Boolean）`

默认： `false`

async的参数是用来判断是否异步导入文件。

#### dumpLineNumbers
类型： `字符串（String）`

参数： `comments`|`mediaQuery`|`all`

默认： `空`

当设置dumpLineNumbers直接输出源行信息到编译好的CSSS的文件中时，有利于你调试指定行。

comments参数用于输出用户可以理解的内容，而mediaQuery使用Firefox一个扩展来解析CSS和抽取信息。

之后我们希望comments能被sourcemaps替代。

#### env
类型： `字符串（String）`

默认： 取决于页面的URL

可以在development或是production环境下运行。

在production环境下，CSS被缓存在本地，消息和信息不能输出到console。

文档的URL开头是“file://”，或是在本地机器中，或是有不标准端口，env的参数将自动设置为development。

例如：
```js
less = { env: 'production' };
```

#### errorReporting
类型： `字符串（String）`

参数： `html`|`console`|`function`

默认： `html`

在LESS编译失败时候，errorReporting会设置错误报告的方法。

#### fileAsync
类型： `布尔值（Boolean）`

默认： `false`

使用文件协议访问页面时异步加载导入的文件。

#### functions
类型： `对象（object）`

在functions这个对象中，key作为函数的名字。

例如：
```js
less = { functions: { myfunc: function() { return 1; }} };
```

functions可以像内置的LESS函数一样使用。

例如：
```less
.my-class {
  border-width: unit(myfunc(), px);
}
```

#### logLevel
类型： `数字（Number）`

默认： 2

javascript控制台日志量（错误等级）。注意：在production环境下，获取不到日志。

```bash
2 - 提示信息（Information）和错误（errors）
1 - 错误（Errors）
0 - 空（Nothing）
```

#### poll
类型： `整型（Integer）`

默认： `1000`

在监视模式下，每两次请求之间的时间间隔（ms）。

#### relativeUrls
类型： `布尔型（Boolean）`

默认： `false`

是否调整相对路径。如果为false，则url已经是相对于入口的LESS文件。

#### globalVars
类型： `对象（Object）`

默认： `undefined`

被注入代码的全局变量列表。对象的主键是变量名，值是变量的值。包括在停止注入的时候，字符串的变量类型必须明确。

#### rootpath
类型： `字符串（String）`

默认： `false`

添加到每个URL开始处的路径。
