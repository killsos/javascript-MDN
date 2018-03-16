**Object.getOwnPropertyDescriptors**

方法用来获取一个对象的所有自身属性的描述符。

## 语法

```
Object.getOwnPropertyDescriptors(obj)
```

### 参数

- `obj`

  任意对象

### 返回值

所指定对象的所有自身属性的描述符，如果没有任何自身属性，则返回空对象。


## 示例

### 浅拷贝一个对象

[`Object.assign()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 方法只能拷贝源对象的可枚举的自身属性，同时拷贝时无法拷贝属性的特性们，而且访问器属性会被转换成数据属性，也无法拷贝源对象的原型，该方法配合 [`Object.create()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create) 方法可以实现上面说的这些。

```
Object.create(
  Object.getPrototypeOf(obj), 
  Object.getOwnPropertyDescriptors(obj) 
);
```

### 创建子类

创建子类的典型方法是定义子类，将其原型设置为超类的实例，然后在该实例上定义属性。这可能会让尴尬，特别是对于 getters 和 setter 而言。 相反，您可以使用此代码设置原型：

```
function superclass() {}
superclass.prototype = {
  // 在这里定义方法和属性
};
function subclass() {}
subclass.prototype = Object.create(superclass.prototype, Object.getOwnPropertyDescriptors({
  // 在这里定义方法和属性
}));
```

## 