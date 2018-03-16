**Object.getPrototypeOf()**

方法返回指定对象的原型（即, 内部`[[Prototype]]`属性的值）。

## 语法

```
Object.getPrototypeOf(object)
```

## 参数

- object

  要返回其原型的对象。

- 返回值给定对象的原型。如果没有继承属性，则返回 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 。

## 示例：

```
let proto = {};
let obj = Object.create(proto);

Object.getPrototypeOf(obj) === proto;
 // true
```

 

## 注释:

在 ES5 中，如果参数不是一个对象类型，将抛出一个  [`TypeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypeError) 异常。在 ES6 /ES2015中，参数被强制转换为一个 [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)**。**

```
> Object.getPrototypeOf("foo");
TypeError: "foo" is not an object  
// ES5 code

> Object.getPrototypeOf("foo");
String.prototype                   
// ES6 code
```