### 长度(length)

> 返回集合中的值的数目.

参数: `list` - 逗号或者空格隔开的值集合。
返回: 集合的值个数。

例如: `length(1px solid #0080ff);`
输出: `3`

例如:

```less
@list: "banana", "tomato", "potato", "peach";
n: length(@list);
```

输出:

```
n: 4;
```

### 提取(extract)

> 返回集合中指定索引的值。

参数:
`list` - 逗号或者空格隔开的值集合。
`index` - 用于返回集合中指定位置值的整型数字。
返回: 集合指定位置处的值。

例如: `extract(8px dotted red, 2);`
输出: `dotted`

例如:

```less
@list: apple, pear, coconut, orange;
value: extract(@list, 3);
```

输出:

```
value: coconut;
```
