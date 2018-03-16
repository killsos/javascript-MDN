# Object.prototype.unwatch()

**警告 :** 请尽量避免使用 unwatch() 和  [`watch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch) . 这两个方法仅在 Gecko 中实现 , 并且他们过去主要作调试用. 另外, 使用 watchpoints 对性能有一系列的副面影响 ，特别是当使用全局对象，如 `window`. 你应该使用  [setters and getters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters) 或 proxies 来替代. 查阅 [Browser compatibility](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/unwatch#Browser_compatibility) 以获取更多信息.

`**unwatch()**` 删除一个 [`watch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch) 设置的 watchpoint.

## 语法

```
obj.unwatch(prop)
```

### 参数

- `prop`

  想要停止监视的对象的属性名

## 描述

JavaScript调试器具有类似的功能，以及其他调试选项。有关调试器的信息  [Venkman](https://developer.mozilla.org/en-US/docs/Venkman).

默认地, 这个方法 被每一个 [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object) 的子类继承 

**Note:** The reason for `unwatch()` to take the property name *prop* as its only parameter is due to the "single handler allowing" behavior of the [`watch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch) method.

## 例子

See [`watch()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/watch).

