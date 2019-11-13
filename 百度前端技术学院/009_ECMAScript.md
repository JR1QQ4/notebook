# JavaScript

JavaScript 是一种脚本，一门编程语言，它可以在网页上实现复杂的功能，网页展现给你的不再是简单的静态信息，而是实时的内容更新，交互式的地图，2D/3D 动画，滚动播放的视频等等。

- HTML是一种标记语言，用来结构化我们的网页内容并赋予内容含义，例如定义段落、标题和数据表，或在页面中嵌入图片和视频。
- CSS 是一种样式规则语言，可将样式应用于 HTML 内容， 例如设置背景颜色和字体，在多个列中布局内容。
- JavaScript 是一种脚本语言，可以用来创建动态更新的内容，控制多媒体，制作图像动画，还有很多。（好吧，虽然它不是万能的，但可以通过简短的代码来实现神奇的功能。）

JavaScript 语言核心之上所构建的功能更令人兴奋。应用程序接口（Application Programming Interfaces（API））将为你的代码提供额外的超能力。

API 通常分为两类。

1.浏览器 API 内建于 web 浏览器中，它们可以使周边计算环境的数据暴露出来，还可以做实用的复杂工作。例如：
-  文档对象模型 API（DOM（Document Object Model）API） 能通过创建、移除和修改 HTML，为页面动态应用新样式等手段来操作 HTML 和 CSS。比如当某个页面出现了一个弹窗，或者显示了一些新内容（像上文小 demo 中看到那样），这就是 DOM 在运行。
-  地理位置 API（Geolocation API） 获取地理信息。这就是为什么 谷歌地图 可以找到你的位置，而且标示在地图上。
-  画布（Canvas） 和 WebGL API 可以创建生动的 2D 和 3D 图像。人们正运用这些 web 技术制作令人惊叹的作品。
-  诸如 HTMLMediaElement 和 WebRTC 等 影音类 API 让你可以利用多媒体做一些非常有趣的事，比如在网页中直接播放音乐和影片，或用自己的网络摄像头获取录像，然后在其他人的电脑上展示。

2.第三方 API 并没有默认嵌入浏览器中，一般要从网上取得它们的代码和信息。比如：
-  Twitter API 和 新浪微博 API 可以在网站上展示最新推文之类。
-  谷歌地图 API 和 高德地图 API 可以在网站嵌入定制的地图等等。

JavaScript 分为内部代码和外部代码。内部代码一般嵌套在</body>之上，用<script></script>script>表示，中间书写代码。外部代码像是外部样式表，需要引入<script src="./main.js"></script>>。

async 和 defer：
- 浏览器遇到 async 脚本时不会阻塞页面渲染，而是直接下载然后运行。这样脚本的运行次序就无法控制，只是脚本不会阻止剩余页面的显示。当页面的脚本之间彼此独立，且不依赖于本页面的其它任何脚本时，async 是最理想的选择。
- 使用 defer 属性，脚本将按照在页面中出现的顺序加载和运行

[文档参考](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/What_is_JavaScript)

## JavaScript历史

大概在 1992 年，一家称作 Nombas 的公司开发了一种叫做 C 减减（C-minus-minus，简称 Cmm）的嵌入式脚本语言。Cmm 背后的理念很简单：一个足够强大可以替代宏操作（macro）的脚本语言，同时保持与 C （和 C ++）足够的相似性，以便开发人员能很快学会。这个脚本语言捆绑在一个叫做 CEnvi 的共享软件中，它首次向开发人员展示了这种语言的威力。

Nombas 最终把 Cmm 的名字改成了 ScriptEase，原因是后面的部分（mm）听起来过于消极，同时字母 C “令人害怕”。现在 ScriptEase 已经成为了 Nombas 产品背后的主要驱动力。

当 Netscape Navigator 崭露头角时，Nombas 开发了一个可以嵌入网页中的 CEnvi 的版本。这些早期的试验被称为 Espresso Page（浓咖啡般的页面），它们代表了第一个在万维网上使用的客户端语言。

当时工作于 Netscape 的 Brendan Eich，开始着手为即将在 1995 年发行的 Netscape Navigator 2.0 开发一个称之为 LiveScript 的脚本语言，当时的目的是在浏览器和服务器（本来要叫它 LiveWire）端使用它。Netscape 与 Sun 及时完成 LiveScript 实现。

就在 Netscape Navigator 2.0 即将正式发布前，Netscape 将其更名为 JavaScript，目的是为了利用 Java 这个因特网时髦词汇。Netscape 的赌注最终得到回报，JavaScript 从此变成了因特网的必备组件。

因为 JavaScript 1.0 如此成功，Netscape 在 Netscape Navigator 3.0 中发布了 1.1 版。恰巧那个时候，微软决定进军浏览器，发布了 IE 3.0 并搭载了一个 JavaScript 的克隆版，叫做 JScript。在微软进入后，有 3 种不同的 JavaScript 版本同时存在：Netscape Navigator 3.0 中的 JavaScript、IE 中的 JScript 以及 CEnvi 中的 ScriptEase。

1997 年，JavaScript 1.1 作为一个草案提交给欧洲计算机制造商协会（ECMA）。第 39 技术委员会（TC39）被委派来“标准化一个通用、跨平台、中立于厂商的脚本语言的语法和语义”。由来自 Netscape、Sun、微软、Borland 和其他一些对脚本编程感兴趣的公司的程序员组成的 TC39 锤炼出了 ECMA-262，该标准定义了名为 ECMAScript 的全新脚本语言。

 ECMAScript 是一个重要的标准，但它并不是 JavaScript 唯一的部分，一个完整的 JavaScript 实现是由以下 3 个不同部分组成的：
 - 核心（ECMAScript）
     + 描述了：语法、类型、语句、关键字、保留字、运算符、对象
 - 文档对象模型（DOM）
     + DOM 通过创建树来表示文档，从而使开发者对文档的内容和结构具有空前的控制力。用 DOM API 可以轻松地删除、添加和替换节点。
 - 浏览器对象模型（BOM）：可以对浏览器窗口进行访问和操作
     + 弹出新的浏览器窗口
     + 移动、关闭浏览器窗口以及调整窗口大小
     + 提供 Web 浏览器详细信息的定位对象
     + 提供用户屏幕分辨率详细信息的屏幕对象
     + 对 cookie 的支持
     + IE 扩展了 BOM，加入了 ActiveXObject 类，可以通过 JavaScript 实例化 ActiveX 对象

[参考文档](http://www.w3school.com.cn/js/pro_js_history.asp)

## ECMAScript

### ECMAScript 基础

1.规范
（1）区分大小写，变量、函数名、运算符以及其他一切东西都是区分大小写的
（2）变量是弱类型的，定义变量时只用 var 运算符
（3）每行结尾的分号可有可无
（4）注释，单行注释以双斜杠开头（//），多行注释以单斜杠和星号开头（/*），以星号和单斜杠结尾（*/）
（5）括号表示代码块

2.变量
（1）声明变量：var test = "hi", age = 25;变量可以存放不同类型的值
（2）命名变量：第一个字符必须是字母、下划线（_）或美元符号（$），余下的字符可以是下划线、美元符号或任何字母或数字字符
（3）著名的变量命名规则：Camel 标记法 - var myTestValue，Pascal 标记法 - var MyTestValue，匈牙利类型标记法 - var iMyTestValue（i 表示整数，s 表示字符串）
（4）变量声明不是必须的：sTest = "hello "，ECMAScript 的解释程序遇到未声明过的标识符时，用该变量名创建一个全局变量，并将其初始化为指定的值。

3.关键字
ECMA-262 定义了 ECMAScript 支持的一套关键字（keyword）。这些关键字标识了 ECMAScript 语句的开头和/或结尾。根据规定，关键字是保留的，不能用作变量名或函数名。
```
break   case   catch   continue   default   delete   do
else   finally   for   function   if   in   instanceof   new
return   switch   this   throw   try   typeof   var   void
while   with
```
如果把关键字用作变量名或函数名，可能得到诸如 "Identifier Expected"（应该有标识符、期望标识符）这样的错误消息。

4.保留字
ECMA-262 定义了 ECMAScript 支持的一套保留字（reserved word）。保留字在某种意思上是为将来的关键字而保留的单词。因此保留字不能被用作变量名或函数名。
```
abstract   boolean   byte   char   class   const   debugger
double   enum   export   extends   final   float   goto   implements
import   int   interface   long   native   package   private
protected   public  short   static   super   synchronized   throws
transient
```
如果将保留字用作变量名或函数名，那么除非将来的浏览器实现了该保留字，否则很可能收不到任何错误消息。当浏览器将其实现后，该单词将被看做关键字，如此将出现关键字错误。

5.原始值和引用值
（1）原始值：存储在栈（stack）中的简单数据段，也就是说，它们的值直接存储在变量访问的位置。
（2）引用值：存储在堆（heap）中的对象，也就是说，存储在变量处的值是一个指针（point），指向存储对象的内存处
（3）原始类型： Undefined、Null、Boolean、Number 和 String 型， typeof 运算符来判断一个值是否在某种类型的范围内
（4）在许多语言中，字符串都被看作引用类型，而非原始类型，因为字符串的长度是可变的。ECMAScript 打破了这一传统。

6.原始类型
ECMAScript 有 5 种原始类型（primitive type），即 Undefined、Null、Boolean、Number 和 String。
（1）typeof 运算符：var sTemp = "test string";alert (typeof sTemp);    //输出 "string"
```
undefined - 如果变量是 Undefined 类型的
boolean - 如果变量是 Boolean 类型的
number - 如果变量是 Number 类型的
string - 如果变量是 String 类型的
object - 如果变量是一种引用类型或 Null 类型的
```
为什么 typeof 运算符对于 null 值会返回 "Object"。这实际上是 JavaScript 最初实现中的一个错误，然后被 ECMAScript 沿用了。现在，null 被认为是对象的占位符，从而解释了这一矛盾，但从技术上来说，它仍然是原始值。

（2）Undefined 类型：当声明的变量未初始化时，该变量的默认值是 undefined。
```
var oTemp;
alert(typeof oTemp);  // 输出 "undefined"
alert(typeof oTemp2);  // 输出 "undefined"

var oTemp;
alert(oTemp2 == undefined);  // 报错

function testFunc() { }
alert(testFunc() == undefined);  // 没有返回值，输出 "true"
```

（3）Null 类型：值 undefined 实际上是从值 null 派生来的，因此 ECMAScript 把它们定义为相等的。
```
alert(null == undefined);  //输出 "true"
```
（4）Boolean 类型：它有两个值 true 和 false （即两个 Boolean 字面量）。

（5）Number 类型：这种类型既可以表示 32 位的整数，还可以表示 64 位的浮点数。
```
var iNum = 070;  //070 等于十进制的 56
var iNum = 0x1f;  //0x1f 等于十进制的 31
var iNum = 0xAB;  //0xAB 等于十进制的 171
var fNum = 5.0; // 对于浮点字面量的有趣之处在于，用它进行计算前，真正存储的是字符串。
var fNum = 5.618e7 // 5.618 x 107
```
当计算生成的数大于 Number.MAX_VALUE 时，它将被赋予值 Number.POSITIVE_INFINITY，意味着不再有数字值。同样，生成的数值小于 Number.MIN_VALUE 的计算也会被赋予值 Number.NEGATIVE_INFINITY，也意味着不再有数字值。

如果计算返回的是无穷大值，那么生成的结果不能再用于其他计算。 Infinity。Number.POSITIVE_INFINITY 的值为 Infinity。Number.NEGATIVE_INFINITY 的值为 -Infinity。

可以对任何数调用 isFinite() 方法，以确保该数不是无穷大。
NaN，表示非数（Not a Number）。NaN 是个奇怪的特殊值。一般说来，这种情况发生在类型（String、Boolean 等）转换失败时。与无穷大一样，NaN 也不能用于算术计算。 
```
alert(NaN == NaN);  //输出 "false"
alert(isNaN("blue"));  //输出 "true"
alert(isNaN("666"));  //输出 "false"
```
（6）String 类型
String 类型的独特之处在于，它是唯一没有固定大小的原始类型。可以用字符串存储 0 或更多的 Unicode 字符，有 16 位整数表示。字符串字面量是由双引号（"）或单引号（'）声明的。
```
var sColor1 = "red";
var sColor2 = 'red';
```
ECMAScript 的字符字面量：
```
\n - 换行
\t - 制表符
\b - 空格
\r - 回车
\f - 换页符
\\ - 反斜杠
\' - 单引号
\" - 双引号
\0nnn  - 八进制代码 nnn 表示的字符（n 是 0 到 7 中的一个八进制数字）
\xnn   - 十六进制代码 nn 表示的字符（n 是 0 到 F 中的一个十六进制数字）
\unnnn - 十六进制代码 nnnn 表示的 Unicode 字符（n 是 0 到 F 中的一个十六进制数字）
```

6.类型转换
（1）转换成字符串
ECMAScript 的 Boolean 值、数字和字符串的原始值的有趣之处在于它们是伪对象，这意味着它们实际上具有属性和方法。
```
var sColor = "red";
alert(sColor.length);   //输出 "3"

var bFound = false;
alert(bFound.toString());   //输出 "false"

// Number 类型的 toString() 方法比较特殊，它有两种模式，即默认模式和基模式。采用默认模式，toString() 方法只是用相应的字符串输出数字值（无论是整数、浮点数还是科学计数法）
var iNum1 = 10;
var iNum2 = 10.0;
alert(iNum1.toString());    //输出 "10"
alert(iNum2.toString());    //输出 "10"

// 基只是要转换成的基数的另一种加法而已
var iNum = 10;
alert(iNum.toString(2));    //输出 "1010"
alert(iNum.toString(8));    //输出 "12"
alert(iNum.toString(16));   //输出 "A"
```
(2)转换成数字
ECMAScript 提供了两种把非数字的原始值转换成数字的方法，即 parseInt() 和 parseFloat()。只有对 String 类型调用这些方法，它们才能正确运行；对其他类型返回的都是 NaN。
```
var iNum1 = parseInt("12345red");   //返回 12345
var iNum1 = parseInt("0xA");    //返回 10
var iNum1 = parseInt("56.9");   //返回 56
var iNum1 = parseInt("red");    //返回 NaN
var iNum1 = parseInt("AF", 16); //返回 175
var iNum1 = parseInt("10", 2);  //返回 2
var iNum2 = parseInt("10", 8);  //返回 8
var iNum3 = parseInt("10", 10); //返回 10
var iNum1 = parseInt("010");    //返回 8
var iNum2 = parseInt("010", 8); //返回 8
var iNum3 = parseInt("010", 10);    //返回 10

var fNum1 = parseFloat("12345red"); //返回 12345
var fNum2 = parseFloat("0xA");  //返回 NaN
var fNum3 = parseFloat("11.2"); //返回 11.2
var fNum4 = parseFloat("11.22.33"); //返回 11.22
var fNum5 = parseFloat("0102"); //返回 102
var fNum1 = parseFloat("red");  //返回 NaN
```
（3）强制类型转换：Boolean(value)、Number(value)、String(value)
```
var b1 = Boolean("");       //false - 空字符串
var b2 = Boolean("hello");      //true - 非空字符串
var b1 = Boolean(50);       //true - 非零数字
var b1 = Boolean(null);     //false - null
var b1 = Boolean(0);        //false - 零
var b1 = Boolean(new object()); //true - 对象

// 如果字符串值能被完整地转换，Number() 将判断是调用 parseInt() 方法还是 parseFloat() 方法。
Number(false)   -    0
Number(true)    -    1
Number(undefined)   -    NaN
Number(null)    -    0
Number("1.2")   -    1.2
Number("12")    -    12
Number("1.2.3") -    NaN
Number(new object())    -    NaN
Number(50)  -    50
```
(4)String() 函数：可把任何值转换成字符串
要执行这种强制类型转换，只需要调用作为参数传递进来的值的 toString() 方法，即把 12 转换成 "12"，把 true 转换成 "true"，把 false 转换成 "false"，以此类推。
```
// 与toString() 方法的唯一不同之处在于，对 null 和 undefined 值强制类型转换可以生成字符串而不引发错误
var s1 = String(null);  //"null"
var oNull = null;
var s2 = oNull.toString();  //会引发错误
```

7.引用类型
（1）引用类型通常叫做类（class），也就是说，遇到引用值，所处理的就是对象。
从传统意义上来说，ECMAScript 并不真正具有类。事实上，除了说明不存在类，在 ECMA-262 中根本没有出现“类”这个词。ECMAScript 定义了“对象定义”，逻辑上等价于其他程序设计语言中的类。
```
var o = new Object();  // 尽管括号不是必需的，但是为了避免混乱，最好使用括号
```

（2）Object 对象
因为 ECMAScript 中的 Object 对象与 Java 中的 java.lang.Object 相似，ECMAScript 中的所有对象都由这个对象继承而来，Object 对象中的所有属性和方法都会出现在其他对象中，所以理解了 Object 对象，就可以更好地理解其他对象。

Object 对象具有下列属性：
-  constructor：对创建对象的函数的引用（指针）。对于 Object 对象，该指针指向原始的 Object() 函数。
-  Prototype：对该对象的对象原型的引用。对于所有的对象，它默认返回 Object 对象的一个实例。

Object 对象还具有几个方法：
-  hasOwnProperty(property)：判断对象是否有某个特定的属性。必须用字符串指定该属性。（例如，o.hasOwnProperty("name")）
-  IsPrototypeOf(object)：判断该对象是否为另一个对象的原型。
-  PropertyIsEnumerable：判断给定的属性是否可以用 for...in 语句进行枚举。
-  ToString()：返回对象的原始字符串表示。对于 Object 对象，ECMA-262 没有定义这个值，所以不同的 ECMAScript 实现具有不同的值。
-  ValueOf()：返回最适合该对象的原始值。对于许多对象，该方法返回的值都与 ToString() 的返回值相同。

（2）Boolean 对象
Boolean 对象是 Boolean 原始类型的引用类型。
```
var oBooleanObject = new Boolean(true); // 传递 Boolean 值作为参数

var oFalseObject = new Boolean(false);
var bResult = oFalseObject && true; //输出 true
```

（3）Number 对象
Number 对象是 Number 原始类型的引用类型。
```
// 得到数字对象的 Number 原始值，只需要使用 valueOf() 方法
var oNumberObject = new Number(68);
var iNumber = oNumberObject.valueOf();

// toFixed() 方法返回的是具有指定位数小数的数字的字符串表示
var oNumberObject = new Number(68);
alert(oNumberObject.toFixed(2));  //输出 "68.00"

//  toExponential() 返回的是用科学计数法表示的数字的字符串形式
var oNumberObject = new Number(68);
alert(oNumberObject.toExponential(1));  //输出 "6.8e+1"

//  toPrecision() 方法根据最有意义的形式来返回数字的预定形式或指数形式
var oNumberObject = new Number(68);
alert(oNumberObject.toPrecision(1));  //输出 "7e+1"
alert(oNumberObject.toPrecision(2));  //输出 "68"
alert(oNumberObject.toPrecision(3));  //输出 "68.0"
```

（4）String 对象
String 对象是 String 原始类型的对象表示法.
```
var oStringObject = new String("hello world");
alert(oStringObject.valueOf() == oStringObject.toString()); //输出 "true"

alert(oStringObject.length);    //输出 "11"

alert(oStringObject.charAt(1)); //输出 "e"
alert(oStringObject.charCodeAt(1)); //输出 "101"，小写字母 "e" 的字符代码

var oStringObject = new String("hello ");
var sResult = oStringObject.concat("world");
alert(sResult);     //输出 "hello world"
alert(oStringObject);   //输出 "hello "

var oStringObject = new String("hello world!");
alert(oStringObject.indexOf("o"));      // 输出 "4"
alert(oStringObject.lastIndexOf("o"));  // 输出 "7"

var oStringObject = new String("yellow");
alert(oStringObject.localeCompare("brick"));   //输出 "1"，排在参数中的字符串之后
alert(oStringObject.localeCompare("yellow"));  //输出 "0"
alert(oStringObject.localeCompare("zoo"));    //输出 "-1"

var oStringObject = new String("hello world");
alert(oStringObject.slice("3"));        //输出 "lo world"
alert(oStringObject.substring("3"));        //输出 "lo world"
alert(oStringObject.slice("3", "7"));       //输出 "lo w"
alert(oStringObject.substring("3", "7"));   //输出 "lo w"
// slice("-3") 转换成 slice("8")，substring("-3") 转换成 substring("0")
alert(oStringObject.slice(-3));       //输出 "rld"
alert(oStringObject.substring(-3));   //输出 "hello world"
alert(oStringObject.slice(3, -4));        //输出 "lo w"
alert(oStringObject.substring(3, -4));    //输出 "hel"

var oStringObject = new String("Hello World");
alert(oStringObject.toLocaleUpperCase());   //输出 "HELLO WORLD"
alert(oStringObject.toUpperCase());     //输出 "HELLO WORLD"
alert(oStringObject.toLocaleLowerCase());   //输出 "hello world"
alert(oStringObject.toLowerCase());     //输出 "hello world"
```

（5）instanceof 运算符
在使用 typeof 运算符时采用引用类型存储值会出现一个问题，无论引用的是什么类型的对象，它都返回 "object"。ECMAScript 引入了另一个 Java 运算符 instanceof 来解决这个问题。
```
// 变量 oStringObject 是否为 String 对象的实例
var oStringObject = new String("hello world");
alert(oStringObject instanceof String); // 输出 "true"
```

### ECMAScript 运算符

1.一元运算符
（1）delete：删除对以前定义的对象属性或方法的引用
delete 运算符不能删除开发者未定义的属性和方法， toString() 方法是原始的 ECMAScript 方法，不是开发者定义的。
```
var o = new Object;
o.name = "David";
alert(o.name);  //输出 "David"
delete o.name;
alert(o.name);  //输出 "undefined"
```

（2）void：对任何值返回 undefined
该运算符通常用于避免输出不应该输出的值，例如，从 HTML 的 <a> 元素调用 JavaScript 函数时。
```
<a href="javascript:window.open('about:blank')">Click me</a>
<a href="javascript:void(window.open('about:blank'))">Click me</a>
```

（3）前增量/前减量运算符
```
var iNum = 10;
++iNum;  // 11 等价于 iNum = iNum + 1；

var iNum = 10;
--iNum;
alert(iNum);    //输出 "9"
alert(--iNum);  //输出 "8"
alert(iNum);    //输出 "8"

var iNum1 = 2;
var iNum2 = 20;
var iNum3 = --iNum1 + ++iNum2;  //等于 "22"
var iNum4 = iNum1 + iNum2;      //等于 "22"
```

（4）后增量/后减量运算符
```
var iNum = 10;
iNum--;
alert(iNum);    //输出 "9"
alert(iNum--);  //输出 "9"
alert(iNum);    //输出 "8"

var iNum1 = 2;
var iNum2 = 20;
var iNum3 = iNum1-- + iNum2++;  //等于 "22"
var iNum4 = iNum1 + iNum2;      //等于 "22"
```

（5）一元加法和一元减法：与高中数学中学到的用法相同
```
var iNum = 20;
iNum = +iNum;
alert(iNum);    //输出 "20"


var sNum = "20";
alert(typeof sNum); //输出 "string"
var iNum = -sNum;
alert(iNum);        //输出 "-20"
alert(typeof iNum); //输出 "number"
```

2.位运算符
位运算符是在数字底层（即表示数字的 32 个数位）进行操作的。
（1）整数
ECMAScript 整数有两种类型，即有符号整数（允许用正数和负数）和无符号整数（只允许用正数）。在 ECMAScript 中，所有整数字面量默认都是有符号整数。

有符号整数使用 31 位表示整数的数值，用第 32 位表示整数的符号，0 表示正数，1 表示负数。数值范围从 -2147483648 到 2147483647。

所有整数字面量都默认存储为有符号整数。只有 ECMAScript 的位运算符才能创建无符号整数
```
var iNum = 18;
alert(iNum.toString(2));    //输出 "10010"
```
负数也存储为二进制代码，不过采用的形式是二进制补码。在处理有符号整数时，开发者不能访问 31 位。
```
var iNum = -18;
alert(iNum.toString(2));    //输出 "-10010"，这是为避免访问位 31
```
把无符号整数转换成字符串后，只返回它们的有效位。

（2）位运算 NOT
```
var iNum1 = 25;     //25 等于 00000000000000000000000000011001
var iNum2 = ~iNum1; //转换为 11111111111111111111111111100110
alert(iNum2);       //输出 "-26"

var iNum1 = 25;
var iNum2 = -iNum1 -1;
alert(iNum2);   //输出 -26
```

（3）位运算 AND
位运算 AND 由和号（&）表示，直接对数字的二进制形式进行运算。
```
var iResult = 25 & 3;
alert(iResult); //输出 "1"

 25 = 0000 0000 0000 0000 0000 0000 0001 1001
  3 = 0000 0000 0000 0000 0000 0000 0000 0011
---------------------------------------------
AND = 0000 0000 0000 0000 0000 0000 0000 0001
```

（4）位运算 OR
位运算 OR 由符号（|）表示，也是直接对数字的二进制形式进行运算。
```
var iResult = 25 | 3;
alert(iResult); //输出 "27"

25 = 0000 0000 0000 0000 0000 0000 0001 1001
 3 = 0000 0000 0000 0000 0000 0000 0000 0011
--------------------------------------------
OR = 0000 0000 0000 0000 0000 0000 0001 1011
```

（5）位运算 XOR
位运算 XOR 由符号（^）表示，当然，也是直接对二进制形式进行运算。
```
var iResult = 25 ^ 3;
alert(iResult); //输出 "26"

 25 = 0000 0000 0000 0000 0000 0000 0001 1001
  3 = 0000 0000 0000 0000 0000 0000 0000 0011
---------------------------------------------
XOR = 0000 0000 0000 0000 0000 0000 0001 1010
```

（6）左移运算
左移运算由两个小于号表示（<<）。它把数字中的所有数位向左移动指定的数量。
```
var iOld = 2;       //等于二进制 10
var iNew = iOld << 5;   //等于二进制 1000000 十进制 64
```

（7）有符号右移运算
有符号右移运算符由两个大于号表示（>>）。它把 32 位数字中的所有数位整体右移，同时保留该数的符号.
```
var iOld = 64;      //等于二进制 1000000
var iNew = iOld >> 5;   //等于二进制 10 十进制 2
```

（8）无符号右移运算
无符号右移运算符由三个大于号（>>>）表示，它将无符号 32 位数的所有数位整体右移。
```
var iOld = 64;      //等于二进制 1000000
var iNew = iOld >>> 5;  //等于二进制 10 十进制 2

var iUnsigned64 = -64 >>> 0;
alert(iUnsigned64.toString(2)); // -64
```

3.逻辑运算符
（1）逻辑 NOT 运算符：由感叹号（!）表示
```
如果运算数是对象，返回 false
如果运算数是数字 0，返回 true
如果运算数是 0 以外的任何数字，返回 false
如果运算数是 null，返回 true
如果运算数是 NaN，返回 true
如果运算数是 undefined，发生错误
```

（2）逻辑 AND 运算符
在 ECMAScript 中，逻辑 AND 运算符用双和号（&&）表示。
```
如果一个运算数是对象，另一个是 Boolean 值，返回该对象。
如果两个运算数都是对象，返回第二个对象。
如果某个运算数是 null，返回 null。
如果某个运算数是 NaN，返回 NaN。
如果某个运算数是 undefined，发生错误。

var bTrue = true;
var bResult = (bTrue && bUnknown);  //发生错误
alert(bResult);         //这一行不会执行

var bFalse = false;
var bResult = (bFalse && bUnknown);
alert(bResult);         //输出 "false"
```

（3）逻辑 OR 运算符：由双竖线（||）表示
```
如果一个运算数是对象，并且该对象左边的运算数值均为 false，则返回该对象。
如果两个运算数都是对象，返回第一个对象。
如果最后一个运算数是 null，并且其他运算数值均为 false，则返回 null。
如果最后一个运算数是 NaN，并且其他运算数值均为 false，则返回 NaN。
如果某个运算数是 undefined，发生错误。
var a = NaN,b = true,c =false,d = null;
c || a  // NaN
a||c  // false
c || d  // null
d || c  // false
```

4.算数运算符
```
如果结果太大或太小，那么生成的结果是 Infinity 或 -Infinity。
如果某个运算数是 NaN，结果为 NaN。
Infinity 乘以 0，结果为 NaN。
Infinity 乘以 0 以外的任何数字，结果为 Infinity 或 -Infinity。
Infinity 乘以 Infinity，结果为 Infinity。
var iResult = 12 * 34;  // 408

如果结果太大或太小，那么生成的结果是 Infinity 或 -Infinity。
如果某个运算数是 NaN，结果为 NaN。
Infinity 被 Infinity 除，结果为 NaN。
Infinity 被任何数字除，结果为 Infinity。
//  0 除一个任何非无穷大的数字，结果为 NaN。
Infinity 被 0 以外的任何数字除，结果为 Infinity 或 -Infinity。
var iResult = 123 / 0;  // Infinity
var iResult = Infinity / 0;  // Infinity

如果被除数是 Infinity，或除数是 0，结果为 NaN。
Infinity 被 Infinity 除，结果为 NaN。
如果除数是无穷大的数，结果为被除数。
如果被除数为 0，结果为 0。
var iResult = Infinity % 0;  // NaN
var iResult = 213 % Infinity;  // 213
var iResult = 0 % 0;  // NaN

某个运算数是 NaN，那么结果为 NaN。
-Infinity 加 -Infinity，结果为 -Infinity。
Infinity 加 -Infinity，结果为 NaN。
+0 加 +0，结果为 +0。
-0 加 +0，结果为 +0。
-0 加 -0，结果为 -0。
Infinity + (-Infinity);  // NaN

某个运算数是 NaN，那么结果为 NaN。
Infinity 减 Infinity，结果为 NaN。
-Infinity 减 -Infinity，结果为 NaN。
Infinity 减 -Infinity，结果为 Infinity。
-Infinity 减 Infinity，结果为 -Infinity。
+0 减 +0，结果为 +0。
-0 减 -0，结果为 -0。
+0 减 -0，结果为 +0。
某个运算符不是数字，那么结果为 NaN。
-0 -0; // -0
```

5.关系运算符
关系运算符小于、大于、小于等于和大于等于执行的是两个数的比较运算，比较方式与算术比较运算相同。
任何包含 NaN 的关系运算符都要返回 false。
```
var bResult1 = 2 > 1    //true
var bResult2 = 2 < 1    //false
var bResult = "Blue" < "alpha";  //输出 true

var bResult = "25" < "3";
alert(bResult); //输出 "true"

var bResult = "25" < 3;
alert(bResult); //输出 "false"

null == undefined      //  true
"NaN" == NaN       //  false
5 == NaN       //  false
NaN == NaN     //  false
NaN != NaN     //  true
false == 0     //  true
true == 1      //  true
true == 2      //  false
undefined == 0     //  false
null == 0      //  false
"5" == 5       //  true

var sNum = "66";
var iNum = 66;
alert(sNum == iNum);    //输出 "true"
alert(sNum === iNum);   //输出 "false"
```

6.条件运算符，三元运算符
```
variable = boolean_expression ? true_value : false_value;
```

7.赋值运算符
```
var iNum = 10;
iNum += 10；  // 等价于 iNum = iNum + 10；
乘法/赋值（*=）  除法/赋值（/=）  取模/赋值（%=）
加法/赋值（+=）  减法/赋值（-=）  
左移/赋值（<<=） 有符号右移/赋值（>>=）  无符号右移/赋值（>>>=）
```

8.逗号运算符：用逗号运算符可以在一条语句中执行多个运算
```
var iNum1 = 1, iNum = 2, iNum3 = 3;
```

### 流程控制

1.if 语句
```
if (condition) statement1 else statement2
if (i > 30)
  {alert("大于 30");}
else
  {alert("小于等于 30");}

if (condition1) statement1 else if (condition2) statement2 else statement3
if (i > 30) {
  alert("大于 30");
} else if (i < 0) {
  alert("小于 0");
} else {
  alert("在 0 到 30 之间");
}
```

2.循环语句
```
do {statement} while (expression);
var i = 0;
do {i += 2;} while (i < 10);

while (expression) statement
var i = 0;
while (i < 10) {
  i += 2;
}

for (initialization; expression; post-loop-expression) statement
iCount = 6;
for (var i = 0; i < iCount; i++) {
  alert(i);
}

for (property in expression) statement  // 用于枚举对象的属性
for (sProp in window) {
  alert(sProp);
}
// PropertyIsEnumerable() 是 ECMAScript 中专门用于说明属性是否可以用 for-in 语句访问的方法
```

3.标签语句
```
label : statement
start : i = 5;
// 标签 start 可以被之后的 break 或 continue 语句引用
```

4.break 和 continue 语句
```
var iNum = 0;
for (var i=1; i<10; i++) {
  if (i % 5 == 0) {    break;  }
  iNum++;
}
alert(iNum);    //输出 "4"

var iNum = 0;
for (var i=1; i<10; i++) {
  if (i % 5 == 0) {    continue;  }
  iNum++;
}
alert(iNum);    //输出 "8"

var iNum = 0;
outermost:
for (var i=0; i<10; i++) {
  for (var j=0; j<10; j++) {
    if (i == 5 && j == 5) { break outermost; }
    iNum++;
  }
}
alert(iNum);    //输出 "55"

var iNum = 0;
outermost:
for (var i=0; i<10; i++) {
  for (var j=0; j<10; j++) {
    if (i == 5 && j == 5) {    continue outermost;  }
    iNum++;
  }
}
alert(iNum);    //输出 "95"
```

5.with 语句：用于设置代码在特定对象中的作用域
```
with (expression) statement
var sMessage = "hello";
with(sMessage) {
  alert(toUpperCase()); //输出 "HELLO"
}
```

6.switch 语句
```
switch (expression)
  case value: statement;
    break;
...
  case value: statement;
    break;
  default: statement;

var BLUE = "blue", RED = "red", GREEN  = "green";
switch (sColor) {  // sColor 没有定义
  case BLUE: alert("Blue");
    break;
  case RED: alert("Red");
    break;
  case GREEN: alert("Green");
    break;
  default: alert("Other");
}
```

### 函数

1.函数概述
```
function functionName(arg0, arg1, ... argN) {
  statements
}
function sayHi(sName, sMessage) {  // 函数声明
  alert("Hello " + sName + sMessage);
}
sayHi("David", " Nice to meet you!"); // 函数调用

function sum(iNum1, iNum2) {
  return iNum1 + iNum2;  // return 声明函数返回值
}
```

2.arguments 对象
在函数代码中，使用特殊对象 arguments，开发者无需明确指出参数名，就能访问它们。
```
function sayHi() {
  if (arguments[0] == "bye") {
    return;
  }
  alert(arguments[0]);
}

//  检测参数个数
function howManyArgs() {
  alert(arguments.length);
}
howManyArgs("string", 45);
howManyArgs();
howManyArgs(12);

// 模拟函数重载
function doAdd() {
  if(arguments.length == 1) {
    alert(arguments[0] + 5);
  } else if(arguments.length == 2) {
    alert(arguments[0] + arguments[1]);
  }
}
doAdd(10);  //输出 "15"
doAdd(40, 20);  //输出 "60"
```

3.Function 对象（类）
Function 类可以表示开发者定义的任何函数。
```
// 每个 arg 都是一个参数，最后一个参数是函数主体（要执行的代码）。这些参数必须是字符串。
var function_name = new function(arg1, arg2, ..., argN, function_body)

function sayHi(sName, sMessage) {
  alert("Hello " + sName + sMessage);
}
// 等价于
var sayHi 
= 
new Function("sName", "sMessage", "alert(\"Hello \" + sName + sMessage);");

function doAdd(iNum) {
  alert(iNum + 10);
}
function sayHi() {
  alert("Hi");
}
alert(doAdd.length);    //输出 "1，参数个数
alert(sayHi.length);    //输出 "0"

//Function 对象也有与所有对象共享的 valueOf() 方法和 toString() 方法。这两个方法返回的都是函数的源代码，在调试时尤其有用。
function doAdd(iNum) {
  alert(iNum + 10);
}
document.write(doAdd.toString());
```

4.闭包（closure）
闭包，指的是词法表示包括不被计算的变量的函数，也就是说，函数可以使用函数之外定义的变量。
```
// 简单的闭包
var sMessage = "hello world";
function sayHelloWorld() {
  alert(sMessage);
}
sayHelloWorld();

// 复杂的闭包
var iBaseNum = 10;
function addNum(iNum1, iNum2) {
  function doAdd() {
    return iNum1 + iNum2 + iBaseNum;
  }
  return doAdd();
}
```

### 面向对象

对象：ECMA-262 把对象（object）定义为“属性的无序集合，每个属性存放一个原始值、对象或函数”。严格来说，这意味着对象是无特定顺序的值的数组。通用的定义是基于代码的名词（人、地点或事物）的表示。

类：每个对象都由类定义，可以把类看做对象的配方。类不仅要定义对象的接口（interface）（开发者访问的属性和方法），还要定义对象的内部工作（使属性和方法发挥作用的代码）。编译器和解释程序都根据类的说明构建对象。

实例：程序使用类创建对象时，生成的对象叫作类的实例（instance）。对类生成的对象的个数的唯一限制来自于运行代码的机器的物理内存。每个实例的行为相同，但实例处理一组独立的数据。由类创建对象实例的过程叫做实例化（instantiation）。

1.面向对象技术
ECMAScript 并没有正式的类。相反，ECMA-262 把对象定义描述为对象的配方。这是 ECMAScript 逻辑上的一种折中方案，因为对象定义实际上是对象自身。即使类并不真正存在，我们也把对象定义叫做类，因为大多数开发者对此术语更熟悉，而且从功能上说，两者是等价的。

（1）面向对象语言的要求
```
封装 - 把相关的信息（无论数据或方法）存储在对象中的能力
聚集 - 把一个对象存储在另一个对象内的能力
继承 - 由另一个类（或多个类）得来类的属性和方法的能力
多态 - 编写能以多种方法运行的函数或方法的能力
```
（2）对象的构成
在 ECMAScript 中，对象由特性（attribute）构成，特性可以是原始值，也可以是引用值。如果特性存放的是函数，它将被看作对象的方法（method），否则该特性被看作对象的属性（property）。

2.对象应用
（1）声明和实例化
```
// 实例化
var oObject = new Object();
var oStringObject = new String();
```

（2）对象引用：在 ECMAScript 中，不能访问对象的物理表示，只能访问对象的引用。每次创建对象，存储在变量中的都是该对象的引用，而不是对象本身。

（3）对象废除
ECMAScript 拥有无用存储单元收集程序（garbage collection routine），意味着不必专门销毁对象来释放内存。当再没有对对象的引用时，称该对象被废除（dereference）了。
```
// 把对象的所有引用都设置为 null，可以强制性地废除对象
var oObject = new Object;
// do something with the object here
oObject = null;
```

（4）早绑定和晚绑定
所谓绑定（binding），即把对象的接口与对象实例结合在一起的方法。早绑定（early binding）是指在实例化对象之前定义它的属性和方法，这样编译器或解释程序就能够提前转换机器代码。ECMAScript 不是强类型语言，所以不支持早绑定。

晚绑定（late binding）指的是编译器或解释程序在运行前，不知道对象的类型。使用晚绑定，无需检查对象的类型，只需检查对象是否支持属性和方法即可。ECMAScript 中的所有变量都采用晚绑定方法。这样就允许执行大量的对象操作，而无任何惩罚。

3.对象类型
在 ECMAScript 中，所有对象并非同等创建的。一般来说，可以创建并使用的对象有三种：本地对象、内置对象和宿主对象。

（1）本地对象
ECMA-262 把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象”。简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。
```
Object   Function   Array   String   Boolean   Number   Date
RegExp   Error   EvalError   RangeError   ReferenceError
SyntaxError   TypeError   URIError
```

（2）内置对象
ECMA-262 把内置对象（built-in object）定义为“由 ECMAScript 实现提供的、独立于宿主环境的所有对象，在 ECMAScript 程序开始执行时出现”。这意味着开发者不必明确实例化内置对象，它已被实例化了。ECMA-262 只定义了两个内置对象，即 Global 和 Math （它们也是本地对象，根据定义，每个内置对象都是本地对象）。

（3）宿主对象
所有非本地对象都是宿主对象（host object），即由 ECMAScript 实现的宿主环境提供的对象。所有 BOM 和 DOM 对象都是宿主对象。

4.对象作用域：作用域指的是变量的适用范围。
（1）公用、私有和受保护作用域
公用作用域中的对象属性可以从对象外部访问，即开发者创建对象的实例后，就可使用它的公用属性。而私有作用域中的属性只能在对象内部访问，即对于外部世界来说，这些属性并不存在。这意味着如果类定义了私有属性和方法，则它的子类也不能访问这些属性和方法。

ECMAScript 只有公用作用域。

建议性的解决方法：许多开发者都在网上提出了有效的属性作用域模式，解决了 ECMAScript 的这种问题。在属性前后加下划线表示私有的：
```
obj._color_ = "blue";
```
有些开发者还喜欢用单下划线说明私有成员，例如：obj._color。

（2）静态作用域：静态作用域定义的属性和方法任何时候都能从同一位置访问。
ECMAScript 没有静态作用域
```
function sayHello() {
  alert("hello");
}
sayHello.alternate = function() {
  alert("hi");
}
sayHello();     //输出 "hello"
sayHello.alternate();   //输出 "hi"
```

（3）关键字 this
关键字 this 总是指向调用该方法的对象：
```
var oCar = new Object;
oCar.color = "red";
oCar.showColor = function() {
  alert(this.color);  // 等价于 alert(oCar.color);
};
oCar.showColor();       //输出 "red"

function showColor() {
  alert(this.color);
};
var oCar1 = new Object;
oCar1.color = "red";
oCar1.showColor = showColor;
var oCar2 = new Object;
oCar2.color = "blue";
oCar2.showColor = showColor;
oCar1.showColor();      //输出 "red"
oCar2.showColor();      //输出 "blue"
```

5.定义类或对象
（1）工厂方式
```
// 原始方式
var oCar = new Object;
oCar.color = "blue";
oCar.doors = 4;
oCar.mpg = 25;
oCar.showColor = function() {
  alert(this.color);
};

// 工厂方式，可以为函数传递参数
function createCar() {
  var oTempCar = new Object;
  oTempCar.color = "blue";
  oTempCar.doors = 4;
  oTempCar.mpg = 25;
  oTempCar.showColor = function() {
    alert(this.color); // 每次调用函数 createCar()，都要创建新函数 showColor()
  };
  return oTempCar;
}
var oCar1 = createCar();
var oCar2 = createCar();

// 工厂方式升级版
function showColor() {
  alert(this.color);
}
function createCar(sColor,iDoors,iMpg) {
  var oTempCar = new Object;
  oTempCar.color = sColor;
  oTempCar.doors = iDoors;
  oTempCar.mpg = iMpg;
  oTempCar.showColor = showColor;
  return oTempCar;
}
```

（2）构造函数方式
```
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.showColor = function() {
    alert(this.color);
  };
}
var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);
```
就像工厂函数，构造函数会重复生成函数，为每个对象都创建独立的函数版本。不过，与工厂函数相似，也可以用外部函数重写构造函数，同样地，这么做语义上无任何意义。这正是下面要讲的原型方式的优势所在。

（3）原型方式
```
function Car() {
}
Car.prototype.color = "blue";
Car.prototype.doors = 4;
Car.prototype.mpg = 25;
Car.prototype.showColor = function() {
  alert(this.color);
};
var oCar1 = new Car();
var oCar2 = new Car();
alert(oCar1 instanceof Car);    //输出 "true",检查给定变量指向的对象的类型
```

（4）混合的构造函数/原型方式
```
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
}
Car.prototype.showColor = function() {
  alert(this.color);
};
var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);
oCar1.drivers.push("Bill");
alert(oCar1.drivers);   //输出 "Mike,John,Bill"
alert(oCar2.drivers);   //输出 "Mike,John"
```

（5）动态原型方法
```
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
  if (typeof Car._initialized == "undefined") {
    Car.prototype.showColor = function() {
      alert(this.color);
    };
    Car._initialized = true;
  }
}
```

（6）混合工厂方式
```
function Car() {
  var oTempCar = new Object;
  oTempCar.color = "blue";
  oTempCar.doors = 4;
  oTempCar.mpg = 25;
  oTempCar.showColor = function() {
    alert(this.color);
  };
  return oTempCar;
}
```

（7）实例
```
var str = "hello ";
str += "world";  // 这个步骤会执行6个步骤，非常浪费资源，造成性能问题

var arr = new Array(); // 使用这个优化代码
arr[0] = "hello ";
arr[1] = "world";
var str = arr.join("");

function StringBuffer () {   // 更好的方法
  this._strings_ = new Array();
}
StringBuffer.prototype.append = function(str) {
  this._strings_.push(str);
};
StringBuffer.prototype.toString = function() {
  return this._strings_.join("");
};
var buffer = new StringBuffer ();
buffer.append("hello ");
buffer.append("world");
var result = buffer.toString();
```

6.修改对象
prototype 属性不仅可以定义构造函数的属性和方法，还可以为本地对象添加属性和方法。

（1）创建新方法
```
Number.prototype.toHexString = function() {  // 添加新方法
  return this.toString(16);
};
var iNum = 15;
alert(iNum.toHexString());      //输出 "F"

Array.prototype.enqueue = function(vItem) {  // 重命名
  this.push(vItem);
};
Array.prototype.dequeue = function() {
  return this.shift();
};

Array.prototype.indexOf = function (vItem) {  // 重构
  for (var i=0; i<this.length; i++) {
    if (vItem == this[i]) {  return i; }
  }
  return -1;
}

Object.prototype.showValue = function () {  // 为本地对象添加新方法
  alert(this.valueOf());
};
```

（2）重定义已有方法
```
Function.prototype.toString = function() {
  return "Function code hidden";
}
function sayHi() {  alert("hi");  }
alert(sayHi.toString());    //输出 "Function code hidden"
```

（3）极晚绑定（Very Late Binding）
从技术上讲，根本不存在极晚绑定。本书采用该术语描述 ECMAScript 中的一种现象，即能够在对象实例化后再定义它的方法。
```
var o = new Object();
Object.prototype.sayHi = function () {
  alert("hi");
};   // 在大多数程序设计语言中，必须在实例化对象之前定义对象的方法。
o.sayHi();
```

### 继承

1.继承机制实例

[几何形状的继承](http://www.w3school.com.cn/i/ct_js_inheritance_in_action.gif)

2.继承机制实现
（1）继承机制
尽管 ECMAScript 并没有像其他语言那样严格地定义抽象类，但有时它的确会创建一些不允许使用的类。通常，我们称这种类为抽象类。

创建的子类将继承超类的所有属性和方法，包括构造函数及方法的实现。记住，所有属性和方法都是公用的，因此子类可直接访问这些方法。子类还可添加超类中没有的新属性和方法，也可以覆盖超类的属性和方法。

和其他功能一样，ECMAScript 实现继承的方式不止一种。这是因为 JavaScript 中的继承机制并不是明确规定的，而是通过模仿实现的。这意味着所有的继承细节并非完全由解释程序处理。

（2）对象冒充
构造函数使用 this 关键字给所有属性和方法赋值（即采用类声明的构造函数方式）。因为构造函数只是一个函数，所以可使 ClassA 构造函数成为 ClassB 的方法，然后调用它。ClassB 就会收到 ClassA 的构造函数中定义的属性和方法。
```
function ClassA(sColor) {
    this.color = sColor;
    this.sayColor = function () {
        alert(this.color);
    };
}
function ClassB(sColor) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;
}

function ClassB(sColor, sName) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;
    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
var objA = new ClassA("blue");
var objB = new ClassB("red", "John");
objA.sayColor();    //输出 "blue"
objB.sayColor();    //输出 "red"
objB.sayName();     //输出 "John"

function ClassZ() {  // 对象冒充可以实现多重继承
    this.newMethod = ClassX;
    this.newMethod();
    delete this.newMethod;

    this.newMethod = ClassY;
    this.newMethod();
    delete this.newMethod;
}
```

（3）call() 方法
call() 方法是与经典的对象冒充方法最相似的方法。它的第一个参数用作 this 的对象。其他参数都直接传递给函数自身。
```
function sayColor(sPrefix,sSuffix) {
    alert(sPrefix + this.color + sSuffix);
};
var obj = new Object();
obj.color = "blue";
sayColor.call(obj, "The color is ", "a very nice color indeed.");

function ClassB(sColor, sName) {
    //this.newMethod = ClassA;
    //this.newMethod(color);
    //delete this.newMethod;
    ClassA.call(this, sColor);
    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
```

（4）apply() 方法
apply() 方法有两个参数，用作 this 的对象和要传递给函数的参数的数组。
```
function sayColor(sPrefix,sSuffix) {
    alert(sPrefix + this.color + sSuffix);
};
var obj = new Object();
obj.color = "blue";
sayColor.apply(obj, new Array("The color is ", "a very nice color indeed."));

function ClassB(sColor, sName) {
    //this.newMethod = ClassA;
    //this.newMethod(color);
    //delete this.newMethod;
    ClassA.apply(this, new Array(sColor)); // ClassA.apply(this, arguments);
    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
```

（5）原型链（prototype chaining）
```
function ClassA() {
}
ClassA.prototype.color = "blue";
ClassA.prototype.sayColor = function () {
    alert(this.color);
};
function ClassB() {
}
ClassB.prototype = new ClassA();

var objB = new ClassB();
alert(objB instanceof ClassA);  //输出 "true"
alert(objB instanceof ClassB);  //输出 "true"
```

（6）混合方式
```
function ClassA(sColor) {
    this.color = sColor;
}
ClassA.prototype.sayColor = function () {
    alert(this.color);
};
function ClassB(sColor, sName) {
    ClassA.call(this, sColor);
    this.name = sName;
}
ClassB.prototype = new ClassA();
ClassB.prototype.sayName = function () {
    alert(this.name);
};

var objA = new ClassA("blue");
var objB = new ClassB("red", "John");
objA.sayColor();    //输出 "blue"
objB.sayColor();    //输出 "red"
objB.sayName(); //输出 "John"
```

[参考文档](http://www.w3school.com.cn/js/index_pro.asp)
