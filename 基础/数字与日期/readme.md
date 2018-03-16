本章节介绍如何掌握Javascript里的数字和日期类型

## 数字

在 JavaScript 里面，数字都是双精度浮点类型的 [double-precision 64-bit binary format IEEE 754](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) （也就是说一个数字只能在 -(253 -1) 和 253 -1之间）。**没有特定的整型数据类型。**除了能够表示浮点数，数字类型有三个符号值: `+`[`Infinity`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)、`-`[`Infinity`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)和 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN) (not-a-number)。参见Javascript指南中的 [JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures) ，了解其他更多的基本类型。

您可以使用四种类型的数字进制：十进制，二进制，八进制和十六进制。

### 十进制数字(Decimal numbers)

```
1234567890
42

// 数字第一个为零的注意事项：

0888 // 888 将被当做十进制处理
0777 // 在非严格格式下会被当做八进制处理 (用十进制表示就是511)
```

请注意，十进制可以以0开头，后面接其他十进制数字，但是假如下一个接的十进制数字小于8，那么该数字将会被当做八进制处理。

### 二进制数字(Binary numbers)

二进制数字语法是以零为开头，后面接一个小写或大写的拉丁文字母B(`0b或者是0B`)。 假如0b后面的数字不是0或者1，那么就会提示这样的语法错误（ `SyntaxError）：` "Missing binary digits after 0b(0b之后缺失二有效的二进制数据)"。

```
var FLT_SIGNBIT  = 0b10000000000000000000000000000000; // 2147483648
var FLT_EXPONENT = 0b01111111100000000000000000000000; // 2139095040
var FLT_MANTISSA = 0B00000000011111111111111111111111; // 8388607
```

### 八进制数字(Octal numbers)

八进制数字语法是以0为开头的。假如0后面的数字不在0到7的范围内，该数字将会被转换成十进制数字。

```
var n = 0755; // 493
var m = 0644; // 420
```

在ECMAScript 5 严格模式下禁止使用八进制语法。八进制语法并不是ECMAScript 5规范的一部分，但是通过在八进制数字添加一个前缀0就可以被所有的浏览器支持：0644 === 420 而且 "\045" === "%"。在ECMAScript 6中使用八进制数字是需要给一个数字添加前缀"0o"。

```
var a = 0o10; // ES6 :八进制
```

### 十六进制(Hexadecimal numbers)

十六进制数字语法是以零为开头，后面接一个小写或大写的拉丁文字母X(`0x或者是0X`)。假如`0x`后面的数字超出规定范围(0123456789ABCDEF)，那么就会提示这样的语法错误(`SyntaxError)：`"Identifier starts immediately after numeric literal".

```
0xFFFFFFFFFFFFFFFFF // 295147905179352830000
0x123456789ABCDEF   // 81985529216486900
0XA                 // 10
```

### 指数形式(Exponentiation)

```
1E3   // 1000
2e6   // 2000000
0.1e2 // 10
```

## `数字对象`

内置的[`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)对象有一些数字化常量属性，如最大值、不是一个数字和无穷大的。你不能改变这些属性的值，但可以按下边的方式使用它们：

```
var biggestNum = Number.MAX_VALUE;
var smallestNum = Number.MIN_VALUE;
var infiniteNum = Number.POSITIVE_INFINITY;
var negInfiniteNum = Number.NEGATIVE_INFINITY;
var notANum = Number.NaN;
```

你永远只用从Number对象引用上边显示的属性，而不是你自己创建的Number对象的属性。

下面的表格汇总了数字对象的属性：

**数字的属性**

| 属性                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`Number.MAX_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_VALUE) | 可表示的最大值                                  |
| [`Number.MIN_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_VALUE) | 可表示的最小值                                  |
| [`Number.NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/NaN) | 特指”非数字“                                  |
| [`Number.NEGATIVE_INFINITY`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/NEGATIVE_INFINITY) | 特指“负无穷”;在溢出时返回                           |
| [`Number.POSITIVE_INFINITY`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/POSITIVE_INFINITY) | 特指“正无穷”;在溢出时返回                           |
| [`Number.EPSILON`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON) | 表示1和比最接近1且大于1的最小[`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)之间的差别 |
| [`Number.MIN_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_SAFE_INTEGER) | JavaScript最小安全整数.                        |
| [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER) | JavaScript最大安全整数.                        |

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`Number.parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/parseFloat) | 把字符串参数解析成浮点数，和全局方法 [`parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) 作用一致. |
| [`Number.parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/parseInt) | 把字符串解析成特定基数对应的整型数字，和全局方法 [`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)作用一致. |
| [`Number.isFinite()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isFinite) | 判断传递的值是否为有限数字。                           |
| [`Number.isInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger) | 判断传递的值是否为整数。                             |
| [`Number.isNaN()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) | 判断传递的值是否为 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN). More robust version of the original global [`isNaN()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN). |
| [`Number.isSafeInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger) | 判断传递的值是否为安全整数。                           |

数字的类型提供了不同格式的方法以从数字对象中检索信息。以下表格总结了 `数字类型原型上的方法。`

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`toExponential()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toExponential) | 返回一个数字的指数形式的字符串，形如：1.23e+2               |
| [`toFixed()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) | 返回指定小数位数的表示形式，var a=123,b=a.toFixed(2)//b="123.00" |
| [`toPrecision()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toPrecision) | 返回一个指定精度的数字。如下例子中，a=123中，3会由于精度限制被迫消失var a=123,b=a.toPrecision(2)//b="1.2e+2" |

## 数学对象

对于内置的[`Math`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)数学常项和函数也有一些属性和方法。 比方说， `Math对象的` `PI` 属性会有属性值 pi (3.141...)，你可以像这样调用它：

```
Math.PI // π
```

同理，标准数学函数也是Math的方法。 这些包括三角函数，对数，指数，和其他函数。比方说你想使用三角函数 `sin`， 你可以这么写：

```
Math.sin(1.56)
```

需要注意的是Math的所有三角函数参数都是弧度制。

下面的表格总结了 `Math` 对象的方法。

Math的方法

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`abs()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/abs) | 绝对值                                      |
| [`sin()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/sin), [`cos()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/cos), [`tan()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/tan) | 标准三角函数;参数为弧度                             |
| [`asin()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/asin), [`acos()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/acos), [`atan()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/atan), [`atan2()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/atan2) | 反三角函数; 返回值为弧度                            |
| [`sinh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/sinh), [`cosh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/cosh), [`tanh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/tanh) | 双曲三角函数; 返回值为弧度.                          |
| [`asinh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/asinh), [`acosh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/acosh), [`atanh()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/atanh) | 反双曲三角函数;返回值为弧度.                          |
| [`pow()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/pow), [`exp()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/exp), [`expm1()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/expm1), [`log10()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/log10), [`log1p()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/log1p), [`log2()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/log2) | 指数与对数函数                                  |
| [`floor()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor), [`ceil()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil) | 返回最大/最小整数小于/大于或等于参数                      |
| [`min()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/min), [`max()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/max) | 返回一个以逗号间隔的数字参数列表中的较小或较大值(分别地)            |
| [`random()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/random) | 返回0和1之间的随机数。                             |
| [`round()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/round), [`fround()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/fround), [`trunc()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/trunc), | 四舍五入和截断函数                                |
| [`sqrt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/sqrt), [`cbrt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/cbrt), [`hypot()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/hypot) | 平方根，立方根，平方参数的和的平方根 两个参数平方和的平方根           |
| [`sign()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/sign) | 数字的符号, 说明数字是否为正、负、零。                     |
| [`clz32()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/clz32),[`imul()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/imul) | 在32位2进制表示中，开头的0的数量.*返回传入的两个参数相乘结果的类C的32位表现形式* |

和其他对象不同，你不能够创建一个自己的Math对象。你只能使用内置的Math对象。

## 日期对象

JavaScript没有日期数据类型。但是你可以在你的程序里使用 [`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date) 对象和其方法来处理日期和时间。Date对象有大量的设置、获取和操作日期的方法。 它并不含有任何属性。

JavaScript 处理日期数据类似于Java。这两种语言有许多一样的处理日期的方法，也都是以1970年1月1日00:00:00以来的毫秒数来储存数据类型的。

`Date` 对象的范围是相对距离 UTC 1970年1月1日 的前后 100,000,000 天。

创建一个日期对象：

```
var dateObjectName = new Date([parameters]);
```

这里的 dateObjectName 对象是所创建的Date对象的一个名字，它可以成为一个新的对象或者已存在的其他对象的一个属性。

不使用 new 关键字来调用Date对象将会简单地将所提供的date对象转换为字符串表示形式。

前边的语法中的参数可以是一下任何一种：

- 无参数 : 创建今天的日期和时间，例如： `today = new Date();`.
- 一个符合以下格式的表示日期的字符串: "月 日, 年 时:分:秒." 例如： `var Xmas95 = new Date("December 25, 1995 13:30:00")。`如果你省略时、分、秒，那么他们的值将被设置为0。
- 一个年，月，日的整型值的集合，例如： `var Xmas95 = new Date(1995, 11, 25)。`
- 一个年，月，日，时，分，秒的集合，例如： `var Xmas95 = new Date(1995, 11, 25, 9, 30, 0);`.

### `Date对象的方法`

处理日期时间的Date对象方法可分为以下几类：

- "set" 方法, 用于设置Date对象的日期和时间的值。
- "get" 方法,用于获取Date对象的日期和时间的值。
- "to" 方法,用于返回Date对象的字符串格式的值。
- parse 和UTC 方法, 用于解析Date字符串。

通过“get”和“set”方法，你可以分别设置和获取秒，分，时，日，星期，月份，年。这里有个getDay方法可以返回星期，但是没有相应的setDay方法用来设置星期，因为星期是自动设置的。这些方法用整数来代表以下这些值：

- 秒，分： 0 至 59
- 时： 0 至 23
- 星期： 0 (周日) 至 6 (周六)
- 日期：1 至 31 
- 月份： 0 (一月) to 11 (十二月)
- 年份： 从1900开始的年数

例如, 假设你定义了如下日期：

```
var Xmas95 = new Date("December 25, 1995");
```

Then `Xmas95.getMonth()` 返回 12, and `Xmas95.getFullYear()` 返回 1995.

`getTime` 和 `setTime` 方法对于比较日期是非常有用的。`getTime`方法返回从1970年1月1日00:00:00的毫秒数。

例如，以下代码展示了今年剩下的天数：

```
var today = new Date();
var endYear = new Date(1995, 11, 31, 23, 59, 59, 999); // 设置日和月，注意，月份是0-11
endYear.setFullYear(today.getFullYear()); // 把年设置为今年
var msPerDay = 24 * 60 * 60 * 1000; // 每天的毫秒数
var daysLeft = (endYear.getTime() - today.getTime()) / msPerDay;
var daysLeft = Math.round(daysLeft); //返回今年剩下的天数

```

这个例子中，创建了一个包含今天的日期的Date对象，并命名为today，然后创建了一个名为endYear的Date对象，并把年份设置为当前年份，接着使用每天的毫秒数和getTime分别获取今天和年底的毫秒数，计算出了今天到年底的天数，最后四舍五入得到今年剩下的天数。

parse方法对于从日期字符串赋值给现有的Date对象很有用，例如：以下代码使用parse和setTime分配了一个日期值给IPOdate对象：

```
var IPOdate = new Date();
IPOdate.setTime(Date.parse("Aug 9, 1995"));
```

### 例子：

在下边的例子中，JSClock()函数返回了用数字时钟格式的时间：

```
function JSClock() {
  var time = new Date();
  var hour = time.getHours();
  var minute = time.getMinutes();
  var second = time.getSeconds();
  var temp = "" + ((hour > 12) ? hour - 12 : hour);
  if (hour == 0)
    temp = "12";
  temp += ((minute < 10) ? ":0" : ":") + minute;
  temp += ((second < 10) ? ":0" : ":") + second;
  temp += (hour >= 12) ? " P.M." : " A.M.";
  return temp;
}
```

`JSClock函数首先创建了一个叫做time的新的Date对象，因为没有参数，所以time代表了当前日期和时间。然后调用了``getHours`, `getMinutes以及getSeconds方法把当前的时分秒分别赋值给了hour`, `minute`,`second。`

接下来的4句在time的基础上创建了一个字符串，第一句创建了一个变量temp，并通过一个条件表达式进行了赋值，如果小时大于12，就为 (`hour - 12`), 其他情况就为 hour, 除非 hour 为 0, 这种情况下，它会变成 12.

接下来的语句拼接了`minute`的值到`temp后。如果minute小于10，条件表达式就会在minute前边加个0，其他情况下加一个分号。然后按同样的方式在temp后拼接上了秒。`

最后，如果hour是12或者更大，条件表达式会在temp后拼接"P.M."，否则拼接"A.M." 。