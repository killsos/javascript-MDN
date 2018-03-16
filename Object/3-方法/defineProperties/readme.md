**Object.defineProperties() **

方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。

## 语法

`Object.defineProperties(*obj*, *props*)`

### 参数

- obj

  将要被添加属性或修改属性的对象

- props

  该对象的一个或多个键值对定义了将要为对象添加或修改的属性的具体配置

## 例子

```
var obj = {};
Object.defineProperties(obj, {
  "property1": {
    value: true,
    writable: true
  },
  "property2": {
    value: "Hello",
    writable: false
  }
  // 等等.
});
alert(obj.property2) //弹出"Hello"
```

## 兼容旧环境（Polyfill）

下面用 `JavaScript` 实现的 `defineProperties` 函数几乎完全等价于原生的 `Object.defineProperties`。

```
function defineProperties(obj, properties)
{
  function convertToDescriptor(desc){
    function hasProperty(obj, prop){
      return Object.prototype.hasOwnProperty.call(obj, prop);
    }

    function isCallable(v){
      // 如果除函数以外,还有其他类型的值也可以被调用,则可以修改下面的语句
      return typeof v === "function";
    }

    if (typeof desc !== "object" || desc === null)
      throw new TypeError("不是正规的对象");

    var d = {};
    if (hasProperty(desc, "enumerable"))
      d.enumerable = !!desc.enumerable;
    if (hasProperty(desc, "configurable"))
      d.configurable = !!desc.configurable;
    if (hasProperty(desc, "value"))
      d.value = desc.value;
    if (hasProperty(desc, "writable"))
      d.writable = !!desc.writable;
    if (hasProperty(desc, "get")){
      var g = desc.get;
      if (!isCallable(g) && g !== "undefined")
        throw new TypeError("bad get");
      d.get = g;
    }
    if (hasProperty(desc, "set")){
      var s = desc.set;
      if (!isCallable(s) && s !== "undefined")
        throw new TypeError("bad set");
      d.set = s;
    }

    if (("get" in d || "set" in d) && ("value" in d || "writable" in d))
      throw new TypeError("identity-confused descriptor");

    return d;
  }

  if (typeof obj !== "object" || obj === null)
    throw new TypeError("不是正规的对象");

  properties = Object(properties);
  var keys = Object.keys(properties);
  var descs = [];
  for (var i = 0; i < keys.length; i++)
    descs.push([keys[i], convertToDescriptor(properties[keys[i]])]);
  for (var i = 0; i < descs.length; i++)
    Object.defineProperty(obj, descs[i][0], descs[i][1]);

  return obj;
}
```