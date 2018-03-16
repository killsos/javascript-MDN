# Object.values()

`**Object.values() **方法返回一个给定对象`自己的`所有可枚举属性值的数组，值的顺序`与`使用`[`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)循环的顺序相同 ( 区别在于for-in循环枚举原型链中的属性 )。

## 语法

```
Object.values(obj)
```

### 参数

- `obj`

  被返回可枚举属性值的对象。

## 描述

`Object.values() 方法返回的数组元素的值和单独访问对象属性的值是一样的。数组元素的值在数组的顺序，和使用 for-in 循环遍历的结果一样。`

## 示例

```
var obj = { foo: "bar", baz: 42 };
console.log(Object.values(obj)); // ['bar', 42]

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.values(obj)); // ['a', 'b', 'c']

// array like object with random key ordering
var an_obj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.values(an_obj)); // ['b', 'c', 'a']

// getFoo is property which isn't enumerable
var my_obj = Object.create({}, { getFoo: { value: function() { return this.foo; } } });
my_obj.foo = "bar";
console.log(Object.values(my_obj)); // ['bar']

// non-object argument will be coerced to an object
console.log(Object.values("foo")); // ['f', 'o', 'o']
```

## Polyfill

为了使不支持  `Object.values() 方法的旧环境兼容 Object.values()，可在 `[tc39/proposal-object-values-entries](https://github.com/tc39/proposal-object-values-entries) 或 [shims/Object.values](https://github.com/es-shims/Object.values) 中找到兼容旧浏览器的方案`。`