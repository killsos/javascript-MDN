# Object.prototype.toLocaleString()

## 概述**toLocaleString()**

方法返回一个该对象的字符串表示。该方法主要用于被本地化相关对象覆盖。

## 语法

```
obj.toLocaleString();
```

## 描述

`Object.toLocaleString`返回调用 [`toString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) 方法的结果。

该函数提供了一个通用的 `toLocaleString` 方法，即使不大可能被用到。见下面列表：

### 覆盖了 toLocaleString() 方法的对象

- `Array`: [`Array.prototype.toLocaleString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)
- `Number`: [`Number.prototype.toLocaleString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)
- `Date`: [`Date.prototype.toLocaleString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)