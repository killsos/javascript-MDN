**Object**

 构造函数创建一个对象包装器。

## 语法

```
// 对象初始化器（Object initialiser）或对象字面量（literal）
{[nameValuePair1[, nameValuePair2[, ...nameValuePairN]]]} 

// 以构造函数形式来调用
new Object([value])
```

### 参数

- `nameValuePair1, nameValuePair2, ... nameValuePair*N*`

  成对的名称（字符串）与值（任何值），其中名称通过冒号与值分隔。

- `value`

  任何值。

## 描述

对象构造函数为给定值创建一个对象包装器。。如果给定值是  [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) or [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)，将会创建并返回一个空对象，否则，将返回一个与给定值对应类型的对象。

当以非构造函数形式被调用时，`Object` 等同于 `new Object()`。

可查看 [对象初始化/字面量语法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Object_initializer)。

## 属性

- `Object.length`

  值为1。


- [`Object.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)

  可以为所有 Object 类型的对象添加属性。

## 方法

- [`Object.assign()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

  通过复制一个或多个对象来创建一个新的对象。

- [`Object.create()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

  指定原型对象和属性来创建一个新的对象。

- [`Object.defineProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

  给对象添加一个属性并指定该属性的配置。

- [`Object.defineProperties()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)

  给对象添加多个属性并分别指定它们的配置。

- [`Object.entries()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) **

  返回一个数组，其是给定对象自身的 enumerable 属性键值`对（[key, value]）。`

- [`Object.freeze()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

  冻结对象：使对象不可删除或修改它的属性。

- [`Object.getOwnPropertyDescriptor()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)

  返回对象指定的属性配置。

- [`Object.getOwnPropertyNames()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)

  返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名。

- [`Object.getOwnPropertySymbols()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols)

  返回一个数组，它包含了指定对象自身所有的符号属性。

- [`Object.getPrototypeOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)

  返回指定对象的原型对象。

- [`Object.is()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

  判断两个值是否严格相等。（类似===运算符，但+0不等于-0，NaN等于自己）。

- [`Object.isExtensible()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible)

  判断对象是否可扩展。

- [`Object.isFrozen()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen)

  判断对象是否已经冻结。

- [`Object.isSealed()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed)

  判断对象是否已经密封。

- [`Object.keys()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

  返回一个数组，包含指定对象的所有自有可遍历属性的名称。

- [`Object.preventExtensions()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)

  阻止对象扩展。

- [`Object.seal()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)

  密封对象以防删除。

- [`Object.setPrototypeOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)

  设置对象的原型。

- [`Object.values()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/values) **

  返回一个数组，其是给定对象自身的 enumerable 属性值。

**对象实例和对象原型对象**

JavaScript语言的所有对象都是由`Object`衍生的对象；所有对象都继承了`Object.prototype`的方法和属性，尽管它们可能被覆盖。例如，其它的构造器原型覆盖了`constructor`属性并提供了其自己的`toString`方法。原型对象的更改会传播给所有的对象，除非这些属性和方法在原型链中被再次覆盖。

### 属性

- [`Object.prototype.constructor`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)

  特定的函数，用于创建一个对象的原型。

- [`Object.prototype.__proto__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__proto__) **

  指向当对象被实例化的时候，用作原型的对象。

- [`Object.prototype.__noSuchMethod__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__noSuchMethod__) **

  当未定义的对象成员被调用作方法的时候，允许定义并执行的函数。

- [`Object.prototype.__count__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__count__) **

  用于直接返回用户定义的对象中可数的属性的数量。已被废除。

- [`Object.prototype.__parent__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__parent__) **

  用于指向对象的内容。已被废除。

### 方法

- [`Object.prototype.__defineGetter__()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__defineGetter__) ** **

  关联一个函数到一个属性。访问该函数时，执行该函数并返回其返回值。

- [`Object.prototype.__defineSetter__()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__defineSetter__) ** **

  关联一个函数到一个属性。设置该函数时，执行该修改属性的函数。

- [`Object.prototype.__lookupGetter__()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__lookupGetter__) ** **

  返回使用 [`__defineGetter__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineGetter) 定义的方法函数 。

- [`Object.prototype.__lookupSetter__()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__lookupSetter__) ** **

  返回使用 [`__defineSetter__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineSetter) 定义的方法函数。

- [`Object.prototype.hasOwnProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)

  返回一个布尔值 ，表示某个对象是否含有指定的属性，而且此属性非原型链继承的。

- [`Object.prototype.isPrototypeOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf)

  返回一个布尔值，表示指定的对象是否在本对象的原型链中。

- [`Object.prototype.propertyIsEnumerable()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/propertyIsEnumerable)

  判断指定属性是否可枚举，内部属性设置参见 [ECMAScript DontEnum attribute](https://developer.mozilla.org/zh-CN/docs/ECMAScript_DontEnum_attribute) 。

- [`Object.prototype.toSource()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toSource) **

  返回字符串表示此对象的源代码形式，可以使用此字符串生成一个新的相同的对象。

- [`Object.prototype.toLocaleString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toLocaleString)

  直接调用 [`toString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)方法。

- [`Object.prototype.toString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

  返回对象的字符串表示。

- [`Object.prototype.unwatch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/unwatch) **

  移除对象某个属性的监听。

- [`Object.prototype.valueOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

  返回指定对象的原始值。

- [`Object.prototype.watch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch) **

  给对象的某个属性增加监听。

- [`Object.prototype.eval()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/eval) **

  在指定对象为上下文情况下执行javascript字符串代码，已经废弃。

## 示例

### 给定 `undefined` 和 `null` 类型使用 `Object`

下面的例子将一个空的 `Object` 对象存到 `o` 中：

```
var o = new Object();
```

```
var o = new Object(undefined);
```

```
var o = new Object(null);
```

### 使用 `Object` 生成布尔对象

下面的例子将[`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean) 对象存到 `o` 中：

```
// 等价于 o = new Boolean(true);
var o = new Object(true);
// 等价于 o = new Boolean(false);
var o = new Object(Boolean());
```