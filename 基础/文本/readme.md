本章介绍在Javascript中如何使用字符串与文本内容.

## 字符串

JavaScript中的 [String](https://developer.mozilla.org/en-US/docs/Glossary/String) 类型用于表示文本型的数据. 它是由无符号整数值（16bit）作为元素而组成的集合. 字符串中的每个元素在字符串中占据一个位置. 第一个元素的index值是0, 下一个元素的index值是1, 以此类推. 字符串的长度就是字符串中所含的元素个数.你可以通过String字面值或者String对象两种方式创建一个字符串.

### String字面值

可以使用单引号或双引号创建简单的字符串:

```
'foo'
"bar"
```

可以使用转义序列来创建更复杂的字符串:

#### 16进制转义序列

\x之后的数值将被认为是一个16进制数.

```
'\xA9' // "©"
```

#### Unicode转义序列

Unicode转义序列在\u之后需要至少4个字符.

```
'\u00A9' // "©"
```

#### Unicode code point escapes

这是ECMAScript 6中的新特性. 有了Unicode code point escapes, 任何字符都可以用16进制数转义, 这使得通过Unicode转义表示大于`0x10FFFF的字符成为可能`. 使用简单的Unicode转义时通常需要分别写字符相应的两个部分（译注：大于0x10FFFF的字符需要拆分为相应的两个小于0x10FFFF的部分）来达到同样的效果.

请参阅 [`String.fromCodePoint()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint) 或 [`String.prototype.codePointAt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/codePointAt).

```
'\u{2F804}'

// the same with simple Unicode escapes
'\uD87E\uDC04'
```

### 字符串对象

[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String) 对象是对原始string类型的封装 .

```
var s = new String("foo"); // Creates a String object
console.log(s); // Displays: { '0': 'f', '1': 'o', '2': 'o'}
typeof s; // Returns 'object'
```

你可以在String字面值上使用String对象的任何方法—JavaScript自动把String字面值转换为一个临时的String对象, 然后调用其相应方法,最后丢弃此临时对象.在String字面值上也可以使用String.length属性.

除非必要, 应该尽量使用String字面值, 因为String对象的某些行为可能并不与直觉一致. 举例:

```
var s1 = "2 + 2"; // Creates a string literal value
var s2 = new String("2 + 2"); // Creates a String object
eval(s1); // Returns the number 4
eval(s2); // Returns the string "2 + 2"
```

`String对象有一个属性`, `length`, 标识了字符串中的字符个数.举例, 下面的代码把13赋值给了`x`, 因为"Hello, World!"包含了13个字符（译注：注意W之前有个空格）:

```
var mystring = "Hello, World!";
var x = mystring.length;
```

`String`对象有许多方法: 举例来说有些方法返回字符串本身的变体, 如 `substring` 和`toUpperCase`.

下表总结了 [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String) 对象的方法.

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`charAt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charAt), [`charCodeAt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt), [`codePointAt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/codePointAt) | 返回字符串指定位置的字符或者字符编码。                      |
| [`indexOf`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf), [`lastIndexOf`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) | 分别返回字符串中指定子串的位置或最后位置。                    |
| [`startsWith`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith), [`endsWith`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith), [`includes`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/includes) | 返回字符串是否以指定字符串开始、结束或包含指定字符串。              |
| [`concat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/concat) | 连接两个字符串并返回新的字符串。                         |
| [`fromCharCode`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode), [`fromCodePoint`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint) | 从指定的Unicode值序列构造一个字符串。这是一个String类方法，不是实例方法。 |
| [`split`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) | 通过将字符串分离成一个个子串来把一个String对象分裂到一个字符串数组中。   |
| [`slice`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/slice) | 从一个字符串提取片段并作为新字符串返回。                     |
| [`substring`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substring), [`substr`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substr) | 分别通过指定起始和结束位置，起始位置和长度来返回字符串的指定子集。        |
| [`match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match), [`replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace), [`search`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search) | 通过正则表达式来工作.                              |
| [`toLowerCase`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase), [`toUpperCase`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) | 分别返回字符串的小写表示和大写表示。                       |
| [`normalize`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/normalize) | 按照指定的一种 Unicode 正规形式将当前字符串正规化。           |
| [`repeat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/repeat) | 将字符串内容重复指定次数后返回。                         |
| [`trim`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/trim) | 去掉字符串开头和结尾的空白字符。                         |

### 多行模板字符串

模板字符串是一种允许内嵌表达式的String字面值. 可以用它实现多行字符串或者字符串内插等特性.

模板字符串使用反勾号 (` `) ([grave accent](https://en.wikipedia.org/wiki/Grave_accent)) 包裹内容而不是单引号或双引号. 模板字符串可以包含占位符. 占位符用美元符号和花括号标识 (`${expression}`).

#### 多行

源代码中插入的任何新行开始字符都作为模板字符串的内容. 使用一般的字符串时, 为了创建多行的字符串不得不用如下语法:

```
console.log("string text line 1\n\
string text line 2");
// "string text line 1
// string text line 2"
```

为了实现同样效果的多行字符串, 现在可以写成如下形式:

```
console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"
```

#### 嵌入表达式

为了在一般的字符串中嵌入表达式, 需要使用如下语法:

```
var a = 5;
var b = 10;
console.log("Fifteen is " + (a + b) + " and\nnot " + (2 * a + b) + ".");
// "Fifteen is 15 and
// not 20."
```

现在, 使用模板字符串, 可以使用语法糖让类似功能的实现代码更具可读性:

```
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and\nnot ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."
```

更多信息, 请阅读 [JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference) 中的 [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings).

## 国际化

[`Intl`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl) 对象是ECMAScript国际化API的命名空间, 它提供了语言敏感的字符串比较，数字格式化和日期时间格式化功能.  [`Collator`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Collator), [`NumberFormat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat), 和 [`DateTimeFormat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat) 对象的构造函数是`Intl`对象的属性.

### 日期和时间格式化

[`DateTimeFormat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat) 对象在日期和时间的格式化方面很有用. 下面的代码把一个日期格式化为美式英语格式. (不同时区结果不同.)

```
var msPerDay = 24 * 60 * 60 * 1000;
 
// July 17, 2014 00:00:00 UTC.
var july172014 = new Date(msPerDay * (44 * 365 + 11 + 197));//2014-1970=44年
//这样创建日期真是醉人。。。还要自己计算天数。。。11是闰年中多出的天数。。。
//197是6×30+16(7月的16天)+3(3个大月)-2(2月少2天)

var options = { year: "2-digit", month: "2-digit", day: "2-digit",
                hour: "2-digit", minute: "2-digit", timeZoneName: "short" };
var americanDateTime = new Intl.DateTimeFormat("en-US", options).format;
 
console.log(americanDateTime(july172014)); // 07/16/14, 5:00 PM PDT
```

### 数字格式化

[`NumberFormat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat) 对象在数字的格式化方面很有用, 比如货币数量值.

```
var gasPrice = new Intl.NumberFormat("en-US",
                        { style: "currency", currency: "USD",
                          minimumFractionDigits: 3 });
 
console.log(gasPrice.format(5.259)); // $5.259

var hanDecimalRMBInChina = new Intl.NumberFormat("zh-CN-u-nu-hanidec",
                        { style: "currency", currency: "CNY" });
 
console.log(hanDecimalRMBInChina.format(1314.25)); // ￥ 一,三一四.二五
```

### 定序

[`Collator`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Collator) 对象在字符串比较和排序方面很有用.

举例, 德语中*有两种不同的排序方式 电话本（phonebook）* 和 字典（*dictionary）*. 电话本排序强调发音, 比如在排序前 “ä”, “ö”等被扩展为 “ae”, “oe”等发音.

```
var names = ["Hochberg", "Hönigswald", "Holzman"];
 
var germanPhonebook = new Intl.Collator("de-DE-u-co-phonebk");
 
// as if sorting ["Hochberg", "Hoenigswald", "Holzman"]:
console.log(names.sort(germanPhonebook.compare).join(", "));
// logs "Hochberg, Hönigswald, Holzman"
```

有些德语词包含变音, 所以在字典中忽略变音进行排序是合理的 (除非待排序的单词只有变音部分不同: *schon* 先于 *schön*).

```
var germanDictionary = new Intl.Collator("de-DE-u-co-dict");
 
// as if sorting ["Hochberg", "Honigswald", "Holzman"]:
console.log(names.sort(germanDictionary.compare).join(", "));
// logs "Hochberg, Holzman, Hönigswald"
```

关于[`Intl`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl) API的更多信息, 请参考 [Introducing the JavaScript Internationalization API](https://hacks.mozilla.org/2014/12/introducing-the-javascript-internationalization-api/).

## 正则表达式

[Regular expressions](https://developer.mozilla.org/en-US/docs/Glossary/Regular_expression) 是用来匹配字符串中字符组合的模式. 它们可以很强大也很复杂, 这在它们自己的章节进行描述. 正则表达式相关的更多内容如下:

- JavaScript指南中的[JavaScript regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).
- [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp) 参考文档.