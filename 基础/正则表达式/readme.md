正则表达式是用于匹配字符串中字符组合的模式。在 JavaScript中，正则表达式也是对象。这些模式被用于 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp) 的 [`exec`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) 和 [`test`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) 方法, 以及 [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String) 的 [`match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)、[`replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)、[`search`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search) 和 [`split`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法。本章介绍 JavaScript正则表达式。

## 创建一个正则表达式

你可以使用以下两种方法之一构建一个正则表达式：

使用一个正则表达式字面量，其由包含在斜杠之间的模式组成，如下所示：

```
/*
   /pattern/flags 
*/

const regex = /ab+c/;

const regex = /^[a-zA-Z]+[0-9]*\W?_$/gi;
```

在加载脚本后，正则表达式字面值提供正则表达式的编译。当正则表达式保持不变时，使用此方法可获得更好的性能。

或者调用`RegExp`对象的构造函数，如下所示：

```
/* 
    new RegExp(pattern [, flags])
*/

let regex = new RegExp("ab+c");

let regex = new RegExp(/^[a-zA-Z]+[0-9]*\W?_$, "gi");

let regex = new RegExp("^[a-zA-Z]+[0-9]*\W?_$", "gi");
```

使用构造函数提供正则表达式的运行时编译。使用构造函数，当你知道正则表达式模式将会改变，或者你不知道模式，并从另一个来源，如用户输入。

## 编写一个正则表达式的模式

一个正则表达式模式是由简单的字符所构成的，比如`/abc/`, 或者是简单和特殊字符的组合，比如 `/ab*c/` 或 `/Chapter (\d+)\.\d*/。后者`用到了括号，它在正则表达式中可以被用作是一个记忆设备。这一部分正则所匹配的字符将会被记住，在后面可以被利用。正如 [使用括号的子字符串匹配](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#使用括号的子字符串匹配)

### 使用简单的模式

简单的模式是有你找到的直接匹配所构成的。比如，`/abc/`这个模式就匹配了在一个字符串中，仅仅字符 'abc' 同时出现并按照这个顺序。在 "Hi, do you know your abc's?" 和 "The latest airplane designs evolved from slabcraft." 就会匹配成功。在上面的两个实例中，匹配的是子字符串 'abc'。在字符串 "Grab crab" 中将不会被匹配，因为它不包含任何的 'abc' 子字符串。

### 使用特殊字符

当你需要搜索一个比直接匹配需要更多条件的匹配时，比如寻找一个或多个 'b'，或者寻找空格，那么这时模式将要包含特殊字符。比如， 模式`/ab*c/`匹配了一个单独的 'a' 后面跟了零个或者多个 'b'（*的意思是前面一项出现了零个或者多个），且后面跟着 'c' 的任何字符组合。在字符串 "cbbabbbbcdebc" 中，这个模式匹配了子字符串 "abbbbc"。

下面的表格列出了一个我们在正则表达式中可以利用的特殊字符的完整列表和描述。

| 字符                                       | 含义                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`\`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backslash) | 匹配将依照下列规则：在非特殊字符之前的反斜杠表示下一个字符是特殊的，不能从字面上解释。例如，没有前面'\'的'b'通常匹配小写'b'，无论它们出现在哪里。如果加了'\',这个字符变成了一个特殊意义的字符，意思是匹配一个[字符边界](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#note)。反斜杠也可以将其后的特殊字符，转义为字面量。例如，模式 /a*/ 代表会匹配 0 个或者多个 a。相反，模式 /a\*/ 将 '*' 的特殊性移除，从而可以匹配像 "a*" 这样的字符串。使用 new RegExp("pattern") 的时候不要忘记将 \ 进行转义，因为 \ 在字符串里面也是一个转义字符。 |
| [`^`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-caret) | 匹配输入的开始。如果多行标志被设置为true，那么也匹配换行符后紧跟的位置。例如，/^A/ 并不会匹配 "an A" 中的 'A'，但是会匹配 "An E" 中的 'A'。当 '^' 作为第一个字符出现在一个字符集合模式时，它将会有不同的含义。[补充字符集合](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#note) 一节有详细介绍和示例。 |
| [`$`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-dollar) | 匹配输入的结束。如果多行标示被设置为true，那么也匹配换行符前的位置。例如，/t$/ 并不会匹配 "eater" 中的 't'，但是会匹配 "eat" 中的 't'。 |
| [`*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-asterisk) | 匹配前一个表达式0次或多次。等价于 {0,}。例如，/bo*/会匹配 "A ghost boooooed" 中的 'booooo' 和 "A bird warbled" 中的 'b'，但是在 "A goat grunted" 中将不会匹配任何东西。 |
| [`+`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-plus) | 匹配前面一个表达式1次或者多次。等价于 {1,}。例如，/a+/匹配了在 "candy" 中的 'a'，和在 "caaaaaaandy" 中所有的 'a'。 |
| [`?`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-questionmark) | 匹配前面一个表达式0次或者1次。等价于 {0,1}。例如，/e?le?/ 匹配 "angel" 中的 'el'，和 "angle" 中的 'le' 以及"oslo' 中的'l'。如果**紧跟在任何量词 \*、 +、? 或 {} 的后面**，将会使量词变为**非贪婪**的（匹配尽量少的字符），和缺省使用的**贪婪模式**（匹配尽可能多的字符）正好相反。例如，对 "123abc" 应用 /\d+/ 将会返回 "123"，如果使用 /\d+?/,那么就只会匹配到 "1"。还可以运用于先行断言，如本表的 `x(?=y)` 和 `x(?!y)` 条目中所述。 |
| [`.`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-dot) | （小数点）匹配除换行符之外的任何单个字符。例如，/.n/将会匹配 "nay, an apple is on the tree" 中的 'an' 和 'on'，但是不会匹配 'nay'。 |
| [`(x)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-capturing-parentheses) | 匹配 'x' 并且记住匹配项，就像下面的例子展示的那样。括号被称为 *捕获括号*。模式 /(foo) (bar) \1 \2/ 中的 '(foo)' 和 '(bar)' 匹配并记住字符串 "foo bar foo bar" 中前两个单词。模式中的 \1 和 \2 匹配字符串的后两个单词。注意 \1、\2、\n 是用在正则表达式的匹配环节。在正则表达式的替换环节，则要使用像 $1、$2、$n 这样的语法，例如，'bar foo'.replace( /(...) (...)/, '$2 $1' )。 |
| [`(?:x)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-capturing-parentheses) | 匹配 'x' 但是不记住匹配项。这种叫作非捕获括号，使得你能够定义为与正则表达式运算符一起使用的子表达式。来看示例表达式 /(?:foo){1,2}/。如果表达式是 /foo{1,2}/，{1,2}将只对 ‘foo’ 的最后一个字符 ’o‘ 生效。如果使用非捕获括号，则{1,2}会匹配整个 ‘foo’ 单词。 |
| [`x(?=y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-lookahead) | 匹配'x'仅仅当'x'后面跟着'y'.这种叫做正向肯定查找。例如，/Jack(?=Sprat)/会匹配到'Jack'仅仅当它后面跟着'Sprat'。/Jack(?=Sprat\|Frost)/匹配‘Jack’仅仅当它后面跟着'Sprat'或者是‘Frost’。但是‘Sprat’和‘Frost’都不是匹配结果的一部分。 |
| [`x(?!y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-look-ahead) | 匹配'x'仅仅当'x'后面不跟着'y',这个叫做正向否定查找。例如，/\d+(?!\.)/匹配一个数字仅仅当这个数字后面没有跟小数点的时候。正则表达式/\d+(?!\.)/.exec("3.141")匹配‘141’但是不是‘3.141’ |
| [`x|y`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-or) | 匹配‘x’或者‘y’。例如，/green\|red/匹配“green apple”中的‘green’和“red apple”中的‘red’ |
| [`{n}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-quantifier) | n是一个正整数，匹配了前面一个字符刚好发生了n次。比如，/a{2}/不会匹配“candy”中的'a',但是会匹配“caandy”中所有的a，以及“caaandy”中的前两个'a'。 |
| [`{n,m}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-quantifier-range) | n 和 m 都是正整数。匹配前面的字符至少n次，最多m次。如果 n 或者 m 的值是0， 这个值被忽略。例如，/a{1, 3}/ 并不匹配“cndy”中得任意字符，匹配“candy”中得a，匹配“caandy”中得前两个a，也匹配“caaaaaaandy”中得前三个a。注意，当匹配”caaaaaaandy“时，匹配的值是“aaa”，即使原始的字符串中有更多的a。 |
| [`[xyz\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-character-set) | 一个字符集合。匹配方括号的中任意字符，包括[转义序列](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types)。你可以使用破折号（-）来指定一个字符范围。对于点（.）和星号（*）这样的特殊符号在一个字符集中没有特殊的意义。他们不必进行转义，不过转义也是起作用的。例如，[abcd] 和[a-d]是一样的。他们都匹配"brisket"中得‘b’,也都匹配“city”中的‘c’。/[a-z.]+/ 和/[\w.]+/都匹配“test.i.ng”中得所有字符。 |
| [`[^xyz\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-character-set) | 一个反向字符集。也就是说， 它匹配任何没有包含在方括号中的字符。你可以使用破折号（-）来指定一个字符范围。任何普通字符在这里都是起作用的。例如，[^abc] 和 [^a-c] 是一样的。他们匹配"brisket"中得‘r’，也匹配“chop”中的‘h’。 |
| [`[\b\]`](hhttps://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backspace) | 匹配一个退格(U+0008)。（不要和\b混淆了。）               |
| [`\b`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-word-boundary) | 匹配一个词的边界。一个词的边界就是一个词不被另外一个词跟随的位置或者不是另一个词汇字符前边的位置。注意，一个匹配的词的边界并不包含在匹配的内容中。换句话说，一个匹配的词的边界的内容的长度是0。（不要和[\b]混淆了）例子：/\bm/匹配“moon”中得‘m’；/oo\b/并不匹配"moon"中得'oo'，因为'oo'被一个词汇字符'n'紧跟着。/oon\b/匹配"moon"中得'oon'，因为'oon'是这个字符串的结束部分。这样他没有被一个词汇字符紧跟着。/\w\b\w/将不能匹配任何字符串，因为一个单词中的字符永远也不可能被一个非词汇字符和一个词汇字符同时紧跟着。**注意:** JavaScript的正则表达式引擎将[特定的字符集](http://www.ecma-international.org/ecma-262/5.1/#sec-15.10.2.6)定义为“字”字符。不在该集合中的任何字符都被认为是一个断词。这组字符相当有限：它只包括大写和小写的罗马字母，小数位数和下划线字符。不幸的是，重要的字符，例如“é”或“ü”，被视为断词。 |
| [`\B`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-word-boundary) | 匹配一个非单词边界。他匹配一个前后字符都是相同类型的位置：都是单词或者都不是单词。一个字符串的开始和结尾都被认为是非单词。例如，/\B../匹配"noonday"中得'oo', 而/y\B./匹配"possibly yesterday"中得’ye‘ |
| [`\c*X*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-control) | 当X是处于A到Z之间的字符的时候，匹配字符串中的一个控制符。例如，`/\cM/` 匹配字符串中的 control-M (U+000D)。 |
| [`\d`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-digit) | 匹配一个数字`。``等价于[0-9]`。例如， `/\d/` 或者 `/[0-9]/` 匹配"B2 is the suite number."中的'2'。 |
| [`\D`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-digit) | 匹配一个非数字字符`。``等价于[^0-9]`。例如， `/\D/` 或者 `/[^0-9]/` 匹配"B2 is the suite number."中的'B' 。 |
| [`\f`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-form-feed) | 匹配一个换页符 (U+000C)。                        |
| [`\n`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-line-feed) | 匹配一个换行符 (U+000A)。                        |
| [`\r`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-carriage-return) | 匹配一个回车符 (U+000D)。                        |
| [`\s`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-white-space) | 匹配一个空白字符，包括空格、制表符、换页符和换行符。等价于[ \f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]。例如, `/\s\w*/` 匹配"foo bar."中的' bar'。 |
| [`\S`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-white-space) | 匹配一个非空白字符。等价于`[^ `\f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff`]`。例如， `/\S\w*/` 匹配"foo bar."中的'foo'。 |
| [`\t`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-tab) | 匹配一个水平制表符 (U+0009)。                      |
| [`\v`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-vertical-tab) | 匹配一个垂直制表符 (U+000B)。                      |
| [`\w`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-word) | 匹配一个单字字符（字母、数字或者下划线）。等价于`[A-Za-z0-9_]`。例如, `/\w/` 匹配 "apple," 中的 'a'，"$5.28,"中的 '5' 和 "3D." 中的 '3'。 |
| [`\W`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-word) | 匹配一个非单字字符。等价于`[^A-Za-z0-9_]`。例如, `/\W/` 或者 `/[^A-Za-z0-9_]/` 匹配 "50%." 中的 '%'。 |
| [`\*n*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backreference) | 当 n 是一个正整数，一个返回引用到最后一个与有n插入的正值表达式(counting left parentheses)匹配的副字符串。比如 `/apple(,)\sorange\1/` 匹配"apple, orange, cherry, peach."中的'apple, orange,' 。 |
| [`\0`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-null) | 匹配 NULL (U+0000) 字符， 不要在这后面跟其它小数，因为 `\0<digits>` 是一个八进制转义序列。 |
| [`\xhh`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-hex-escape) | 与代码 hh 匹配字符（两个十六进制数字）                    |
| [`\uhhhh`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-unicode-escape) | 与代码 hhhh 匹配字符（四个十六进制数字）。                 |

| [`\u{hhhh}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions$edit#special-unicode-escape-es6) | (仅当设置了u标志时) 使用Unicode值hhhh匹配字符 (十六进制数字). |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

将用户输入转义为正则表达式中的一个字面字符串, 可以通过简单的替换来实现：

```
function escapeRegExp(string){
    return string.replace(/([.*+?^=!:${}()|[\]\/\\])/g, "\\$&"); 
    //$&表示整个被匹配的字符串
}
```

### 使用插入语

任何正则表达式的插入语都会使这部分匹配的副字符串被记忆。一旦被记忆，这个副字符串就可以被调用于其它用途，如同 [使用括号的子字符串匹配](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#使用括号的子字符串匹配)之中所述。

比如， `/Chapter (\d+)\.\d*/` 解释了额外转义的和特殊的字符，并说明了这部分pattern应该被记忆。它精确地匹配后面跟着一个以上数字字符的字符 'Chapter '  (`\d` 意为任何数字字符，`+ 意为1次以上`)，跟着一个小数点（在这个字符中本身也是一个特殊字符；小数点前的 \ 意味着这个pattern必须寻找字面字符 '.')，跟着任何数字字符0次以上。 (`\d` 意为数字字符， `*` 意为0次以上)。另外，插入语也用来记忆第一个匹配的数字字符。

此模式可以匹配字符串"Open Chapter 4.3, paragraph 6"，并且'4'将会被记住。此模式并不能匹配"Chapter 3 and 4"，因为在这个字符串中'3'的后面没有点号'.'。

括号中的"?:"，这种模式匹配的子字符串将不会被记住。比如，(?:\d+)匹配一次或多次数字字符，但是不能记住匹配的字符。

## 使用正则表达式[**EDIT](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions$edit#使用正则表达式)

正则表达式可以被用于`RegExp`的[`exec`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/exec)和[`test`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/test)方法以及 [`String`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String)的[`match`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/match)、[`replace`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/replace)、[`search`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/search)和[`split`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/split)方法。这些方法在[JavaScript 手册](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference)中有详细的解释。

| 方法        | 描述                                       |
| --------- | ---------------------------------------- |
| `exec`    | 一个在字符串中执行查找匹配的RegExp方法，它返回一个数组（未匹配到则返回null）。 |
| `test`    | 一个在字符串中测试是否匹配的RegExp方法，它返回true或false。    |
| `match`   | 一个在字符串中执行查找匹配的String方法，它返回一个数组或者在未匹配到时返回null。 |
| `search`  | 一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者在失败时返回-1。 |
| `replace` | 一个在字符串中执行查找匹配的String方法，并且使用替换字符串替换掉匹配到的子字符串。 |
| `split`   | 一个使用正则表达式或者一个固定字符串分隔一个字符串，并将分隔后的子字符串存储到数组中的String方法。 |

当你想要知道在一个字符串中的一个匹配是否被找到，你可以使用test或search方法；想得到更多的信息（但是比较慢）则可以使用exec或match方法。如果你使用exec或match方法并且匹配成功了，那么这些方法将返回一个数组并且更新相关的正则表达式对象的属性和预定义的正则表达式对象（详见下）。如果匹配失败，那么exec方法返回null（也就是false）。

在接下来的例子中，脚本将使用exec方法在一个字符串中查找一个匹配。

```
var myRe = /d(b+)d/g;
var myArray = myRe.exec("cdbbdbsbz");
```

如果你不需要访问正则表达式的属性，这个脚本通过另一个方法来创建myArray：

```
var myArray = /d(b+)d/g.exec("cdbbdbsbz");
```

如果你想通过一个字符串构建正则表达式，那么这个脚本还有另一种方法：

```
var myRe = new RegExp("d(b+)d", "g");
var myArray = myRe.exec("cdbbdbsbz");
```

通过这些脚本，匹配成功后将返回一个数组并且更新正则表达式的属性，如下表所示。

| 对象        | 属性或索引                                    | 描述                                       | 在例子中对应的值         |
| --------- | ---------------------------------------- | ---------------------------------------- | ---------------- |
| `myArray` |                                          | 匹配到的字符串和所有被记住的子字符串。                      | `["dbbd", "bb"]` |
| `index`   | 在输入的字符串中匹配到的以0开始的索引值。                    | `1`                                      |                  |
| `input`   | 初始字符串。                                   | `"cdbbdbsbz"`                            |                  |
| `[0]`     | 匹配到的所有字符串（并不是匹配后记住的字符串）。注：原文"The last matched characters."，应该是原版错误。匹配到的最后一个字符索引。 | `"dbbd"`                                 |                  |
| `myRe`    | `lastIndex`                              | 下一个匹配的索引值。（这个属性只有在使用g参数时可用在 [通过参数进行高级搜索](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#.E9.80.9A.E8.BF.87.E5.8F.82.E6.95.B0.E8.BF.9B.E8.A1.8C.E9.AB.98.E7.BA.A7.E6.90.9C.E7.B4.A2) 一节有详细的描述.) | `5`              |
| `source`  | 模式文本。在正则表达式创建时更新，不执行。                    | `"d(b+)d"`                               |                  |

在这个例子中如第二种形式所示，你可以使用一个正则表达式创建一个没有分配给变量的对象初始化容器。如果你这样做，那么，每一次使用时都好比在使用一个新的正则表达式。因为这个原因，如果你使用这个未分配给一个变量的正则表达式，你将在随后不能访问这个正则表达式的属性。例如，假如你有如下脚本：

```
var myRe = /d(b+)d/g;
var myArray = myRe.exec("cdbbdbsbz");
console.log("The value of lastIndex is " + myRe.lastIndex);
```

这个脚本输出如下：

```
The value of lastIndex is 5
```

然而，如果你有如下脚本：

```
var myArray = /d(b+)d/g.exec("cdbbdbsbz");
console.log("The value of lastIndex is " + /d(b+)d/g.lastIndex);
```

它显示为：

```
The value of lastIndex is 0
```

当发生/d(b+)d/g使用两个不同状态的正则表达式对象，lastIndex属性会得到不同的值。如果你需要访问一个正则表达式的属性，则需要创建一个对象初始化生成器，你应该首先把它赋值给一个变量。

### 使用括号的子字符串匹配

一个正则表达式模式使用括号，将导致相应的子匹配被记住。例如，/a(b)c /可以匹配字符串“abc”，并且记得“b”。回调这些括号中匹配的子串，使用数组元素[1],……[n]。

使用括号匹配的子字符串的数量是无限的。返回的数组中保存所有被发现的子匹配。下面的例子说明了如何使用括号的子字符串匹配。

下面的脚本使用replace()方法来转换字符串中的单词。在匹配到的替换文本中，脚本使用替代的$ 1,$ 2表示第一个和第二个括号的子字符串匹配。

```
var re = /(\w+)\s(\w+)/;
var str = "John Smith";
var newstr = str.replace(re, "$2, $1");
console.log(newstr);
```

这个表达式输出 "Smith, John"。

### 通过标志进行高级搜索

正则表达式有四个可选参数进行全局和不分大小写搜索。这些参数既可以单独使用也可以一起使用在任何顺序和包含正则表达式的部分中。

| 标志   | 描述                                |
| ---- | --------------------------------- |
| `g`  | 全局搜索。                             |
| i    | 不区分大小写搜索。                         |
| m    | 多行搜索。                             |
| y    | 执行“粘性”搜索,匹配从目标字符串的当前位置开始，可以使用y标志。 |

包含一个标志的正则表达式，使用这个表达式：

```
var re = /pattern/flags;
```

或者

```
var re = new RegExp("pattern", "flags");
```

值得注意的是，标志是一个正则表达式的一部分，它们在接下来的时间将不能添加或删除。

例如，re = /\w+\s/g 将创建一个查找一个或多个字符后有一个空格的正则表达式，或者组合起来像此要求的字符串。

```
var re = /\w+\s/g;
var str = "fee fi fo fum";
var myArray = str.match(re);
console.log(myArray);
```

这段代码将输出 ["fee ", "fi ", "fo "]。在这个例子中，你可以将：

```
var re = /\w+\s/g;
```

替换成：

```
var re = new RegExp("\\w+\\s", "g");
```

并且能获取到相同的结果。

m标志用于指定多行输入字符串应该被视为多个行。如果使用m标志，^和$匹配的开始或结束输入字符串中的每一行，而不是整个字符串的开始或结束。

## 例子

以下例子说明了一些正值表达式的用途。

### 改变输入字符串的顺序

以下例子解释了正值表达式的构成和`string.split()` 以及 `string.replace()的用途。它会整理一个只有粗略格式的含有全名（名字首先出现）的输入字符串，这个字符串被空格、换行符和一个分号分隔。`最终，它会颠倒名字顺序（姓氏首先出现）和list的类型。

```
// The name string contains multiple spaces and tabs,
// and may have multiple spaces between first and last names.
var names = "Harry Trump ;Fred Barney; Helen Rigby ; Bill Abel ; Chris Hand ";

var output = ["---------- Original String\n", names + "\n"];

// Prepare two regular expression patterns and array storage.
// Split the string into array elements.

// pattern: possible white space then semicolon then possible white space
var pattern = /\s*;\s*/;

// Break the string into pieces separated by the pattern above and
// store the pieces in an array called nameList
var nameList = names.split(pattern);

// new pattern: one or more characters then spaces then characters.
// Use parentheses to "memorize" portions of the pattern.
// The memorized portions are referred to later.
pattern = /(\w+)\s+(\w+)/;

// New array for holding names being processed.
var bySurnameList = [];

// Display the name array and populate the new array
// with comma-separated names, last first.
//
// The replace method removes anything matching the pattern
// and replaces it with the memorized string—second memorized portion
// followed by comma space followed by first memorized portion.
//
// The variables $1 and $2 refer to the portions
// memorized while matching the pattern.

output.push("---------- After Split by Regular Expression");

var i, len;
for (i = 0, len = nameList.length; i < len; i++){
  output.push(nameList[i]);
  bySurnameList[i] = nameList[i].replace(pattern, "$2, $1");
}

// Display the new array.
output.push("---------- Names Reversed");
for (i = 0, len = bySurnameList.length; i < len; i++){
  output.push(bySurnameList[i]);
}

// Sort by last name, then display the sorted array.
bySurnameList.sort();
output.push("---------- Sorted");
for (i = 0, len = bySurnameList.length; i < len; i++){
  output.push(bySurnameList[i]);
}

output.push("---------- End");

console.log(output.join("\n"));
```

### 用特殊字符检验输入

在以下例子中，我们期望用户输入一个电话号码。当用户点击“Check”按钮，我们的脚本开始检查这些数字是否合法。如果数字合法（匹配正值表达式所规定的字符序列），脚本显示一条感谢用户的信息并确认该数字。如果这串数字不合法，脚本提示用户电话号码不合法。.

包含非捕获括号 `(?:` 这个正值表达式寻找三个数字字符`\d{3}` 或者 `|` 一个左半括号`\(`跟着三位数字`\d{3}`, 跟着一个封闭括号 `\)`, (结束非捕获括号 `)`)， 后跟着一个短破折号或左斜杠或小数点，随后跟随三个数字字符，当记忆字符 `([-\/\.])捕获并记住，后面跟着三位小数` `\d{3}，再后面跟随记住的左斜杠、右斜杠或小数点` `\1，最后跟着四位小数` `\d{4}。`

当用户按下Enter设置RegExp.input，这些变化也能被激活。

```
<!DOCTYPE html>
<html>  
  <head>  
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">  
    <meta http-equiv="Content-Script-Type" content="text/javascript">  
    <script type="text/javascript">  
      var re = /(?:\d{3}|\(\d{3}\))([-\/\.])\d{3}\1\d{4}/;  
      function testInfo(phoneInput) {  
        var OK = re.exec(phoneInput.value);  
        if (!OK)  
          window.alert(phoneInput.value + ' isn\'t a phone number with area code!');  
        else
          window.alert('Thanks, your phone number is ' + OK[0]);  
      }  
    </script>  
  </head>  
  <body>  
    <p>Enter your phone number (with area code) and then click "Check".
        <br>The expected format is like ###-###-####.</p>
    <form action="#">  
      <input id="phone"><button onclick="testInfo(document.getElementById('phone'));">Check</button>
    </form>  
  </body>  
</html>
```