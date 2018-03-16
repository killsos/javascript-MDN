**Object.getOwnPropertySymbols()**

方法会返回一个数组，该数组包含了指定对象自身的（非继承的）所有 symbol 属性键。

## 语法

```
Object.getOwnPropertySymbols(obj)
```

### 参数

- obj

  任意一个对象

## 描述

该方法和 [`Object.getOwnPropertyNames()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames) 类似，但后者返回的结果只会包含字符串类型的**属性键**，也就是传统的**属性名**。

## 示例

```
var obj = {};
var a = Symbol("a");
var b = Symbol.for("b");

obj[a] = "localSymbol";
obj[b] = "globalSymbol";

var objectSymbols = Object.getOwnPropertySymbols(obj);

console.log(objectSymbols.length); // 2
console.log(objectSymbols)         // [Symbol(a), Symbol(b)]
console.log(objectSymbols[0])      // Symbol(a)
```

## 