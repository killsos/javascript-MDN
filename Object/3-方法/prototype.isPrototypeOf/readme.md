# Object.prototype.isPrototypeOf()

**isPrototypeOf()** 方法用于测试一个对象是否存在于另一个对象的原型链上。

Note: isPrototypeOf() 与 [`instanceof`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)  运算符不同。在表达式 "`object instanceof AFunction`"中，对象原型链是针对 AFunction.prototype 进行检查的，而不是针对 `AFunction` 本身。

 

## 语法

```
prototypeObj.isPrototypeOf(object)
```

### 参数

- object

  在该对象的原型链上搜寻

### 返回值

[`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean)，表示调用对象是否在另一个对象的原型链上。

## 描述

## `isPrototypeOf `方法允许你检查一个对象是否存在于另一个对象的原型链上。

例如，考虑下面的原型链：

```
function Fee() {
  // . . .
}

function Fi() {
  // . . .
}
Fi.prototype = new Fee();

function Fo() {
  // . . .
}
Fo.prototype = new Fi();

function Fum() {
  // . . .
}
Fum.prototype = new Fo();
```

下面创建一个 `Fum `实例，检测 `Fi.prototype `是否存在于该实例的原型链上。

```
var fum = new Fum();
. . .

if (Fi.prototype.isPrototypeOf(fum)) {
  // do something safe
}
```

当需要判断对象的后代是否在特定原型链上，例如，以保证一定的方法或属性将存在该对象上，这时候就需要用到 [`instanceof`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)。