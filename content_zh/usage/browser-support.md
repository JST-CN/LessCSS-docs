---
title: 浏览器支持
---

LESS只支持在现代浏览器中运行（最新版本的Chrome, Firefox, Safari 和 IE）。我们不建议在生产环境中使用LESS客户端，因为在将LESS编译成CSS的时候，用户会看到加载延迟的现象，即便在浏览器中有不足一秒的加载延迟，但也会降低性能。另外，如果在Javascrip执行错误的时候，还会引起美观问题。

某些情况下在生产环境中使用LESS客户端是合理的，例如你想让用户去调整影响主题的LESS变量，然后你想将这些LESS变量实时展示给他们看，在这种情况下，你就不用担心要等待样式更新之后才能让他们看到调整之后的Less变量。

LESS1.4不再包含es5-shim，因此要兼容IE低版本，请在引用less.js之前手工引入[es5-shim.js](https://github.com/kriskowal/es5-shim)。
