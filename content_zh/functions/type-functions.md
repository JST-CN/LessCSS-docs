### 函数(isnumber)

> 如果一个值是一个数字，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是数字返回真`true`,否则假`false`.

例如:

```less
isnumber(#ff0);     // false
isnumber(blue);     // false
isnumber("string"); // false
isnumber(1234);     // true
isnumber(56px);     // true
isnumber(7.8%);     // true
isnumber(keyword);  // false
isnumber(url(...)); // false
```


### 函数(isstring)

> 如果一个值是一个字符串，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是字符串返回真`true`,否则假`false`.

例如:

```less
isstring(#ff0);     // false
isstring(blue);     // false
isstring("string"); // true
isstring(1234);     // false
isstring(56px);     // false
isstring(7.8%);     // false
isstring(keyword);  // false
isstring(url(...)); // false
```


### 函数(iscolor)

> 如果一个值是一个颜色，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是颜色返回真`true`,否则假`false`.

例如:

```less
iscolor(#ff0);     // true
iscolor(blue);     // true
iscolor("string"); // false
iscolor(1234);     // false
iscolor(56px);     // false
iscolor(7.8%);     // false
iscolor(keyword);  // false
iscolor(url(...)); // false
```


### 函数(iskeyword)

> 如果一个值是一个关键字，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是关键字返回真`true`,否则假`false`.

例如:

```less
iskeyword(#ff0);     // false
iskeyword(blue);     // false
iskeyword("string"); // false
iskeyword(1234);     // false
iskeyword(56px);     // false
iskeyword(7.8%);     // false
iskeyword(keyword);  // true
iskeyword(url(...)); // false
```


### 函数(isurl)

>  如果一个值是一个url地址，返回'真(true)',否则返回'假(false)'.

参数: `value` -  待判断的值或变量.

返回: 若是url返回真'true',否则假'false'.

例如:

```less
isurl(#ff0);     // false
isurl(blue);     // false
isurl("string"); // false
isurl(1234);     // false
isurl(56px);     // false
isurl(7.8%);     // false
isurl(keyword);  // false
isurl(url(...)); // true
```


### 函数(ispixel)

> 如果一个值是带像素长度单位的数字，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是带px单位的数字返回真`true`,否则假`false`.

例如:

```less
ispixel(#ff0);     // false
ispixel(blue);     // false
ispixel("string"); // false
ispixel(1234);     // false
ispixel(56px);     // true
ispixel(7.8%);     // false
ispixel(keyword);  // false
ispixel(url(...)); // false
```


### 函数(isem)

> 如果一个值是带em长度单位的数字，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是带em单位的数字返回真`true`,否则假`false`.

例如:

```less
isem(#ff0);     // false
isem(blue);     // false
isem("string"); // false
isem(1234);     // false
isem(56px);     // false
isem(7.8em);    // true
isem(keyword);  // false
isem(url(...)); // false
```


### 函数(ispercentage)

> 如果一个值是带百分比单位的数字，返回'真(true)',否则返回'假(false)'.

参数: `value` - 待判断的值或变量.

返回: 若是带百分比单位的数字返回真`true`,否则假`false`.

例如:

```less
ispercentage(#ff0);     // false
ispercentage(blue);     // false
ispercentage("string"); // false
ispercentage(1234);     // false
ispercentage(56px);     // false
ispercentage(7.8%);     // true
ispercentage(keyword);  // false
ispercentage(url(...)); // false
```


### 函数(isunit)

> 如果一个值是带指定单位的数字，返回'真(true)',否则返回'假(false)'.

参数:
* `value` - 待判断的值或变量.
* `unit` -  用于测试比较的一个单位标示符.

返回: 若是带指定单位的数字返回真`true`,否则假`false`.
例如:

```less
isunit(11px, px);  // true
isunit(2.2%, px);  // false
isunit(33px, rem); // false
isunit(4rem, rem); // true
isunit(56px, "%"); // false
isunit(7.8%, '%'); // true
isunit(1234, em);  // false
isunit(#ff0, pt);  // false
isunit("mm", mm);  // false
```
