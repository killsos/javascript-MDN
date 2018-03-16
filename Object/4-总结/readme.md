1. preventExtensions()

* 不能添加新属性
* 可以删除属性
* 可以在对象原型上添加属性
* 可以修改属性值

2. seal()

* 不能添加新属性
* 对configurable设为false
* 不可删除属性
* 对于属性的描述writable为true,依然可以修改属性值
  ​

3. freeze()

* 不能添加新属性

* 不能修改属性值

* 不能删除属性

* 不能修改configurable

  ​

