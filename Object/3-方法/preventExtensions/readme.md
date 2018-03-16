**Object.preventExtensions()**方法让一个对象变的不可扩展，也就是永远不能再添加新的属性。

## 语法

```
Object.preventExtensions(obj)
```

### 参数

- obj

  将要变得不可扩展的对象

## 描述

如果一个对象可以添加新的属性，则这个对象是可扩展的。`preventExtensions` 可以让这个对象变的不可扩展，也就是不能再有新的属性。需要注意的是不可扩展的对象的属性通常仍然可以被删除。尝试给一个不可扩展对象添加新属性的操作将会失败，不过可能是静默失败，也可能会抛出 [`TypeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypeError) 异常（[严格模式](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Functions_and_function_scope/Strict_mode)）。

`Object.preventExtensions` 只能阻止一个对象不能再添加新的自身属性，仍然可以为该对象的原型添加属性。然而Object.preventExtensions会阻止一个对象将__proto__属性重新指向另一个对象。

在 ECMAScript 5 中可扩展的对象可以变得不可扩展，但反过来不行。

## 例子

```
// Object.preventExtensions将原对象变的不可扩展,并且返回原对象.
var obj = {};
var obj2 = Object.preventExtensions(obj);
assert(obj === obj2);
 
// 字面量方式定义的对象默认是可扩展的.
var empty = {};
assert(Object.isExtensible(empty) === true);
 
// ...但可以改变.
Object.preventExtensions(empty);
assert(Object.isExtensible(empty) === false);
 
// 使用Object.defineProperty方法为一个不可扩展的对象添加新属性会抛出异常.
var nonExtensible = { removable: true };
Object.preventExtensions(nonExtensible);
Object.defineProperty(nonExtensible, "new", { value: 8675309 }); // 抛出TypeError异常
 
// 在严格模式中,为一个不可扩展对象的新属性赋值会抛出TypeError异常.
function fail()
{
  "use strict";
  nonExtensible.newProperty = "FAIL"; // throws a TypeError
}
fail();
 
// 一个不可扩展对象的原型是不可更改的,__proto__是个非标准魔法属性,可以更改一个对象的原型.
var fixed = Object.preventExtensions({});
fixed.__proto__ = { oh: "hai" }; // 抛出TypeError异常
```