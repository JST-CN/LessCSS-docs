---
title: 浏览器支持
---

Less只支持在现代浏览器中运行（最新版本的Chrome, Firefox, Safari 和 IE）。我们不鼓励在生产环境中使用客户端的用法，因为在把Less编译成CSS的时候，用户会看到加载延迟，即便在浏览器有不足一秒的延迟也会降低性能，另外，如果在Javascrip执行错误的时候，还会引起美观问题。

某些情况下在生产环境中使用less客户端是合理的，例如你想让用户去调整影响主题的Less变量，然后将这些Less变量实时展示给他们看，在这种情况下，用户就不用担心在等待样式更新之后才能让他们看到调整之后的Less变量。

如果你想在低版本的浏览器中运行Less,需要引入一个能增加less所需Javascript功能的 [es-5 shim](https://github.com/kriskowal/es5-shim)。
