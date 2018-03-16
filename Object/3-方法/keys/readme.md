**Object.keys()** 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和使用 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环遍历该对象时返回的顺序一致 （两者的主要区别是 一个 for-in 循环还会枚举其原型链上的属性）。

## 语法

```
Object.keys(obj)
```

## 参数

- obj

  要返回其枚举自身属性的对象。

- 返回值一个表示给定对象的所有可枚举属性的字符串数组。

## 描述

`Object.keys` 返回一个所有元素为字符串的数组，其元素来自于从给定的对象上面可直接枚举的属性。这些属性的顺序与手动遍历该对象属性时的一致。

## 例子

```
var arr = ["a", "b", "c"];
alert(Object.keys(arr)); 
// 弹出"0,1,2"

/* 类数组对象 */ 
var obj = { 0 : "a", 1 : "b", 2 : "c"};
alert(Object.keys(obj)); 
// 弹出"0,1,2"
```

```
/* 具有随机键排序的数组类对象 */
var an_obj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(an_obj)); 
// console: ['2', '7', '100']
```

```
/* getFoo是个不可枚举的属性 */ 
var my_obj = Object.create(
   {}, 
   { getFoo : { value : function () { return this.foo } } }
);
my_obj.foo = 1;

alert(Object.keys(my_obj)); 
// 只弹出foo
```

如果你想获取一个对象的所有属性,，甚至包括不可枚举的，请查看[`Object.getOwnPropertyNames`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)。

## 注意

在ES5，如果此方法的参数不是一个对象（原始的），那么它会造成 TypeError。在ES2015，非对象的参数将被强制转换为一个对象。

```
Object.keys("foo");
// TypeError: "foo" is not an object (ES5 code)

Object.keys("foo");
// ["0", "1", "2"]                   (ES2015 code)
```

## Polyfill

要在原生不支持的旧环境中添加兼容的Object.keys，请复制以下代码段：

```
if (!Object.keys) {
  Object.keys = (function () {
    var hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({toString: null}).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;

    return function (obj) {
      if (typeof obj !== 'object' && typeof obj !== 'function' || obj === null) throw new TypeError('Object.keys called on non-object');

      var result = [];

      for (var prop in obj) {
        if (hasOwnProperty.call(obj, prop)) result.push(prop);
      }

      if (hasDontEnumBug) {
        for (var i=0; i < dontEnumsLength; i++) {
          if (hasOwnProperty.call(obj, dontEnums[i])) result.push(dontEnums[i]);
        }
      }
      return result;
    }
  })()
};
```

上面的代码在IE7（也许IE8也是）下有个问题，就是如果传入一个来自其他 window 对象下的对象时，不可枚举的属性也会获取到。

另一个简单点的实现方法，来自 [Javascript - Object.keys Browser Compatibility](http://tokenposts.blogspot.com.au/2012/04/javascript-objectkeys-browser.html)

```
if (!Object.keys) Object.keys = function(o) {
  if (o !== Object(o))
    throw new TypeError('Object.keys called on a non-object');
  var k=[],p;
  for (p in o) if (Object.prototype.hasOwnProperty.call(o,p)) k.push(p);
  return k;
}
```

## 