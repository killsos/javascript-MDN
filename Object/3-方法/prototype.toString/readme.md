# Object.prototype.toString()

`**toString()**` 方法返回一个表示该对象的字符串

## 语法

```
object.toString()
```

## 返回值

一个表示该对象的字符串

## 描述

每个对象都有一个 toString() 方法，当对象被表示为文本值时或者当以期望字符串的方式引用对象时，该方法被自动调用。默认情况下，toString() 方法被每个继承自`Object`的对象继承。如果此方法在自定义对象中未被覆盖，`toString()` 返回 "[object *type*]",其中type是对象类型。以下代码说明了这一点：

```
let obj = new Object();

obj.toString();           
// 返回 [object Object]
```

**Note:** 从JavaScript 1.8.5开始，用`null调用``toString()方法会返回``[object *Null*]，`类似的用`undefined调用`会返回`[object *Undefined*], `如在ECMAScript的第5版中定义的和后续的勘误表。查看[使用toString方法检测对象类型](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/Object/toString#Using_toString_to_detect_object_type)一文了解详情.

## 示例

### 覆盖(遮蔽)默认的`toString`方法

可以自定义一个方法来取代默认的 `toString()` 方法。该 `toString()` 方法不能传入参数并且必须返回一个字符串。自定义的 `toString()` 方法可以是任何我们需要的值，但如果它附带有关对象的信息，它将变的非常有用。

在下面的代码中，定义了一个 `Dog`  对象数据类型，并且创建了该对象的一个实例：

```
function Dog(name,breed,color,sex) {
   this.name=name;
   this.breed=breed;
   this.color=color;
   this.sex=sex;
}

var theDog = new Dog("Gabby","Lab","chocolate","female");
```

如果当前的对象调用了 `toString()` 方法，它将会返回从 `Object 继承下来的` `toString()` 方法的返回默认值：

```
theDog.toString(); // 返回 [object Object]
```

下面的代码中定义了一个叫做 `dogToString()` 的方法来覆盖默认的 `toString()` 方法。这个方法生成一个 "property = value" 形式的字符串，该字符串包含了当前对象的 name， breed，color 和 sex的值。

```
Dog.prototype.toString = function dogToString() {
  var ret = "Dog " + this.name + " is a " + this.sex + " " + this.color + " " + this.breed;
  return ret;
}
```

有了上面的这段代码之后，在上下文中任何时候使用 `theDog` ，JavaScript 都会自动调用 `dogToString()` 方法，并且返回下面的字符串内容：

```
Dog Gabby is a female chocolate Lab
```

### 使用toString()方法来检测对象类型

可以通过`toString()` 来获取每个对象的类型。为了每个对象都能通过 `Object.prototype.toString()` 来检测，需要以 `Function.prototype.call()` 或者 `Function.prototype.apply()` 的形式来调用，把需要检测的对象作为第一个参数传入。

```
var toString = Object.prototype.toString;

toString.call(new Date); // [object Date]
toString.call(new String); // [object String]
toString.call(Math); // [object Math]

//Since JavaScript 1.8.5
toString.call(undefined); // [object Undefined]
toString.call(null); // [object Null]
```

## 