---
published: false
---

> 变量如何求值

## 提示和技巧(Tips & Tricks)

引用自: [less/less.js/issues/1472]({{ site.coderepo }}/issues/1472#issuecomment-22213697)

这里有一个定义变量，然后将它们抑制在私有作用域，阻止它们暴露到全局作用域的技巧。

```less
& {
  // Vars
  @height: 100px;
  @width: 20px;
  // 不要在这个作用域中定义任何属性：值(因为这样做会产生(错误)输出)
  .test {
    height: @height;
    width: @width;
  }
}

.rest {
  height: @height; // Name error: 变量 @height 未定义
}
```

这里，`@height`和`@width`仅仅定义在由`& {...}`创建的作用域中，还可以在规则内嵌套一个作用域。

```less
.some-module {
  @height: 200px;
  @width: 200px;
  text-align: left;
  line-height: @height; // 200px

  & {
    // 重写原来的值
    @height: 100px;
    @width: auto;

    .some-module__element {
      height: @height; // 100px
      width: @width; // 200px
    }

    .some-module__element .text {
      line-height: (@height / 2); // 50px
    }
  }

  & {
    // 重写原来的值
    @height: 50px;

    .some-module__another-element {
      height: @height; // 50px
      width: @width; // 200px
    }

    .some-module__another-element .text {
      line-height: (@height / 2); // 25px
    }
  }
}
```