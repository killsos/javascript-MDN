**Object.entries() **

方法返回一个给定对象自己的可枚举属性[key，value]对的数组，数组中键值对的排列顺序和使用 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环遍历该对象时返回的顺序一致（区别在于一个for-in循环也枚举原型链中的属性）。

## 语法

```
Object.entries(obj)
```

### 参数

- `obj`

  返回该对象由可枚举属性名和对应属性值组成的的键值对。

- 返回值一个给定对象自己的枚举属性[key，value]对的数组。

## 描述

Object.entries() 返回一个所有元素为键值对的数组，其中键值对来自于给定的对象上面可直接枚举属性的属性名与属性值，这些键值对的顺序以键（属性名）为参考，与手动遍历该对象属性时的一致。

## 示例

```
var obj = { foo: "bar", baz: 42 };
console.log(Object.entries(obj)); 
// [ ['foo', 'bar'], ['baz', 42] ]

// 类数组对象
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.entries(obj)); 
// [ ['0', 'a'], ['1', 'b'], ['2', 'c'] ]

// 带有随机（非顺序）排列属性名的类数组对象
var an_obj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.entries(an_obj)); 
// [ ['2', 'b'], ['7', 'c'], ['100', 'a'] ]

// getFoo是不可枚举属性
var my_obj = Object.create(
   {}, 
   { getFoo: { value: function() { return this.foo; } } }
);
my_obj.foo = "bar";
console.log(Object.entries(my_obj)); 
// [ ['foo', 'bar'] ]

// 非对象参数会被强行视为对象
console.log(Object.entries("foo")); 
// [ ['0', 'f'], ['1', 'o'], ['2', 'o'] ]
```

### 将Object转化为Map对象

[`new Map()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map) 构造函数接受一个包含键值对元素的可迭代数组。 借助Object.entries方法你可以很容易的将[`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)转换为[`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map):

```
var obj = { foo: "bar", baz: 42 }; 
var map = new Map(Object.entries(obj));
console.log(map); // Map { foo: "bar", baz: 42 }
```

## Polyfill

为了兼容那些原生不支持Object.entries方法的旧环境，你可以在[tc39/proposal-object-values-entries](https://github.com/tc39/proposal-object-values-entries)或[es-shims/Object.entries](https://github.com/es-shims/Object.entries)找到一些解决方案。