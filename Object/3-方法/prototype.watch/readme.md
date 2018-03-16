# Object.prototype.watch()

**非标准**
该特性是非标准的，请尽量不要在生产环境中使用它！

## 概述

监视一个对象的某个属性是否被赋值,在该属性赋值时触发指定的回调函数.

| Method of [`Object`](https://developer.mozilla.org/zh-cn/JavaScript/Reference/Global_Objects/Object) |                  |
| ---------------------------------------- | ---------------- |
| Implemented in                           | JavaScript 1.8.6 |
| ECMAScript Edition                       | none             |

## 语法

`*object*.watch(*prop*, *handler*)`

## 参数

- `prop`

  想要监视值是否发生变化的指定对象的某个属性的属性名称


- `handler`

  当指定的属性发生变化时执行的回调函数

## 描述

**警告:** 通常来讲,你应该尽量避免使用 `watch()`和 [`unwatch()`](https://developer.mozilla.org/zh-cn/JavaScript/Reference/Global_Objects/Object/unwatch) 方法 . 这两个方法仅在Gecko中实现,并且它们主要是为了在调试的时候使用. In addition, using watchpoints has a serious negative impact on performance, which is especially true when used on global objects, such as window. You can usually use [setters and getters](https://developer.mozilla.org/zh-cn/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters) or proxies instead. See [Compatibility](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch#Compatibility) for details.

Watches for assignment to a property named `prop` in this object, calling `handler(prop, oldval, newval)` whenever `prop` is set and storing the return value in that property. A watchpoint can filter (or nullify) the value assignment, by returning a modified `newval` (or by returning `oldval`).

If you delete a property for which a watchpoint has been set, that watchpoint does not disappear. If you later recreate the property, the watchpoint is still in effect.

To remove a watchpoint, use the `unwatch()` method. By default, the `watch` method is inherited by every object descended from `Object`.

The JavaScript debugger has functionality similar to that provided by this method, as well as other debugging options. For information on the debugger, see [Venkman](https://developer.mozilla.org/zh-cn/Venkman).

In Firefox, `handler` is only called from assignments in script, not from native code. For example, `window.watch('location', myHandler)` will not call `myHandler` if the user clicks a link to an anchor within the current document. However, `window.location += '#myAnchor'` will call `myHandler`.

**注意:** Calling `watch()` on an object for a specific property overrides and previous handler attached for that property.

## 例子

### 例子: 使用 `watch` 和 `unwatch`

```
var o = {p:1};
o.watch("p",
  function (id, oldval, newval) {
    console.log("o." + id + "由" + oldval + " 变为 " + newval);
    return newval;
  });

o.p = 2;
o.p = 3;
delete o.p;
o.p = 4;

o.unwatch('p');
o.p = 5;
```

上面的代码显示结果如下:

```
o.p 由 1 变为 2
o.p 由 2 变为 3
o.p 由 undefined 变为 4
```

### 例子: 使用 `watch` 来验证一个对象的属性

你可以使用 `watch` 来检测一个对象的属性赋值是否是合法的.下例演示了如何确保每个人始终具有一个合法的名字和0 到 200之间的年龄.

```
Person = function(name,age) {
  this.watch("age", Person.prototype._isValidAssignment);
  this.watch("name", Person.prototype._isValidAssignment);
  this.name = name;
  this.age = age;
}

Person.prototype.toString = function() {
  return this.name + ", " + this.age;
};

Person.prototype._isValidAssignment = function(id, oldval, newval) {
  if (id === "name" && (!newval || newval.length > 30)) {
    throw new RangeError("不合法的名字 " + this);
  }
  if (id === "age"  && (newval < 0 || newval > 200)) {
    throw new RangeError("不合法的年龄 " + this);
  }
  return newval;
}

will = new Person("Will", 29);
print(will);   // Will, 29

try {
  will.name = "";
} catch (e) {
  //print(e);
  console.log(e);
}

try {
  will.age = -4;
} catch (e) {
  //print(e);
  console.log(e);
}
```

上面的代码显示结果如下:

```
Will, 29
RangeError: 不合法的名字 Will, 29
RangeError: 不合法的年龄 Will, 29
```

## 兼容性

- [Polyfill](https://gist.github.com/384583) 在所有的支持`ES5`的浏览器上提供了`watch`方法.
- Using a [Proxy](https://developer.mozilla.org/zh-cn/JavaScript/Reference/Global_Objects/Proxy) enables you do that even deeper changes to how property assignments work

## 相关链接

[unwatch()](https://developer.mozilla.org/zh-cn/JavaScript/Reference/Global_Objects/Object/unwatch)