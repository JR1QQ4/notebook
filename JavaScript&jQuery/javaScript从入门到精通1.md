> 今日心灵鸡汤：“你一定得认识到自己想往哪个方向发展，然后一定要对准那个方向出发，要马上。你再也浪费不起多一秒的时间了，你浪费不起。”

## JavaScript基础
演示 js 的网站：
[impress](http://impress.github.io/impress.js/)
[naotu](http://naotu.baidu.com/ )
[codecombat](https://codecombat.com/)
[codemao](https://ide.codemao.cn/)
[google](https://developers.google.com/blockly/)
[blockly-games](https://blockly-games.appspot.com)
[blockly](https://blockly.uieee.com/)

### JavaScript介绍
创始人 Brendan Eich(布莱登.艾奇)，Netscape在最初将其脚本语言命名为LiveScript，后来Netscape在与Sun合作之后将其改名为JavaScript。JavaScript最初受Java启发而开始设计的，目的之一就是“看上去像Java”，因此语法上有类似之处，一些名称和命名规范也借自Java。JavaScript与Java名称上的近似，是当时Netscape为了营销考虑与Sun微系统达成协议的结果。Java和JavaScript的关系就像张雨和张雨生的关系，只是名字很像。
Java  服务器端的编程语言，JavaScript  运行在客户端(浏览器)的编程语言。

JavaScript是一种运行在***客户端*** 的***脚本语言*** 。JavaScript的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。最初的目的是为了处理表单的验证操作。

javascript 是什么？
* 是一门脚本语言：不需要编译，直接运行
* 是一门解释性的语言：遇到一行代码就解释一行代码
* 是一门动态类型的语言：代码只有执行到声明的时候才知道存储的是什么，如果是对象，就有对象的属性和方法；对象没有什么，可以通关点语法为对象添加属性或方法。
* 是一门基于对象的语言：对象具有三大特性，封装、继承、多态
* 是一门弱类型的语言：强类型语言，比如定义变量，需要特定的类型 int,float,double

#### JavaScript现在的意义(应用场景)

1. 网页特效
2. 服务端开发(Node.js)
3.  命令行工具(Node.js)
4. 桌面程序(Electron)
5. App(Cordova)
6. 控制硬件-物联网(Ruff)
7. 游戏开发(cocos2d-js)

#### JavaScript和HTML、CSS的区别

1. HTML：提供网页的结构，提供网页中的内容\
2. CSS: 用来美化网页
3. JavaScript: 可以用来控制网页内容，给网页增加动态的效果

#### JavaScript 的组成

![JavaScript 的组成](./images/1496912475691.png)
1. ECMAScript - JavaScript 的核心：ECMA 欧洲计算机制造联合会，描述了语言的基本语法和数据类型，ECMAScript 是一套标准，定义了一种语言的标准与具体实现无关
2. BOM - 浏览器对象模型：一套操作浏览器功能的 API，通过 BOM 可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等
3. DOM - 文档对象模型：一套操作页面元素的 API，DOM 可以把 HTML 看做是文档树，通过 DOM 提供的 API 可以对树上的节点进行操作

#### JavaScript的书写位置 
* 写在行内：```<input type="button" value="按钮" onclick="alert('Hello World')" />```
* 写在script标签中：```<head><script>alert('Hello World!');</script></head>```
* 写在外部js文件中，在页面引入：```<script src="main.js"></script>```

### 变量
变量是计算机内存中存储数据的标识符，根据变量名称可以获取到内存中存储的数据。使用变量可以方便的获取或者修改内存中的数据。
1. var声明变量：```var age;```
2. 变量的赋值：```var age;  age = 18;```
3. 同时声明多个变量：```var age, name, sex; age = 10; name = 'cjr';```
4. 同时声明多个变量并赋值：```var age = 10, name = 'cjr';```
5. 交换两个变量的值：```var a,b;a=10;b=20;```
	* 方法一：```var temp; temp = b; b=a; a=temp; ```
	* 方法二：```a = a + b; b = a - b; a = a - b;```
	* 方法三(异或)：```a = a ^ b; b = a ^ b; a = a ^ b;```

#### 变量的命名规则和规范
* 规则 - 必须遵守的，不遵守会报错
	* 由字母、数字、下划线、$符号组成，不能以数字开头
	* 不能是关键字和保留字，例如：for、while
	* 区分大小写
* 规范 - 建议遵守的，不遵守不会报错
	* 变量名必须有意义
	* 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。例如：userName、userPassword

#### 注释
1. 单行注释：用来描述下面一个或多行代码的作用
```javascript
// 这是一个变量
var name = 'hm';
```
2. 多行注释：用来注释多条代码
```javascript
/*
var age = 18;
var name = 'zs';
console.log(name, age); 
*/     
/** 还有注释是这个样子的，一般用来注释代码的作用
@type {Console}
*/
```

### 数据类型
原始数据类型：number，string，boolean，null，undefined，Symbol (ECMAScript 6 新定义)，object


#### Number 类型
* 数值字面量：数值的固定值的表示法，20  10215 20.36
* 进制：十进制、十六进制(0xFA)、八进制(024；var i=20;i.toString(8);// 24)
* 浮点数：
	* var n = 5e-324;   // 科学计数法  5乘以10的-324次方
	* 浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数
	* var result = 0.1 + 0.2;    // 结果不是 0.3，而是：0.30000000000000004
	* 不要判断两个浮点数是否相等
* 数值范围
	* 最小值：Number.MIN_VALUE，这个值为： 5e-324
	* 最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
	* 无穷大：Infinity
	* 无穷小：-Infinity
* 数值判断
	* NaN：not a number ，```NaN 与任何值都不相等，包括他本身```
	* isNaN: is not a number，***不要用 NaN 验证是不是 ==NaN，用  isNaN()***

#### String 类型
* 字符串字面量：'abc'   "abc"
* 转义符
 
 ![转义符](./images/1498289626813.png)
* 字符串长度：length属性用来获取字符串的长度
```javascript
var str = 'Hello World';  console.log(str.length);
```
* 字符串拼接，使用 **+** 连接
	```javascript
	console.log(11 + 11);
	console.log('hello' + ' world');
	console.log('11' + 11);
	console.log('male:' + true);
	```
	* 两边只要有一个是字符串，那么 “+” 就是字符串拼接功能	
	* 两边如果都是数字，那么就是算术功能。

#### Boolean 类型
* Boolean字面量：  true和false，区分大小写
* 计算机内部存储：true为1，false为0

#### Undefined 和 Null
1. undefined 表示一个声明了没有赋值的变量，变量只声明的时候值默认是 undefined；函数没有明确返回值，如果接收了，结果也是 undefined。
	* undefined 的变量和一个数字相加，结果是 NaN
2. nul l表示一个空，变量的值如果想为 null，必须手动设置

#### 复杂数据类型 Object

#### 获取变量的类型
* typeof 函数可以获取变量的数据类型
```javascript
var age = 18;   console.log(typeof age);  // 'number'
```

#### 字面量
在源代码中一个固定值的表示法。
数值字面量：8, 9, 10；字符串字面量："Hello World!" ；布尔字面量：true，false。

### 数据类型转换
字符串的颜色是黑色的，数值类型是蓝色的，布尔类型也是蓝色的，undefined和null是灰色的。

#### 转换成数值类型
* parseInt()
```javascript
var num1 = parseInt("12.3abc");  // 返回12，如果第一个字符是数字会解析知道遇到非数字结束
var num2 = parseInt("abc123");   // 返回NaN，如果第一个字符不是数字或者符号就返回NaN
```
* parseFloat()
```javascript
console.log(parseFloat("12.045fsd"));  //12.045
console.log(parseFloat("dasd41531"));  //NaN
// parseFloat会解析第一个. 遇到第二个.或者非数字结束。如果解析的内容里只有整数，解析成整数
```
* Number()
```javascript
console.log(Number("1521dasd"));  //NaN
console.log(Number("dasd123"));  //NaN
// Number()可以把任意值转换成数值，如果要转换的字符串中有一个不是数值的字符，返回NaN
```
* 隐式转换
```javascript
console.log("11" * 2); //22
console.log("22" - 10); //12
console.log("12" + 10); //1210字符串
var str = '500'; console.log(-str); //-500      console.log(+str); // 500
```

#### 转换成字符串类型
* toString()
```javascript
var num = 5;
console.log(num.toString());  // 5 字符串
console.log(null.toString());  // 报错
```
* String()
```javascript
console.log(String(null));   //null
console.log(String(undefined));  //undefined
```
* String() 函数存在的意义：有些值没有 toString()，这个时候可以使用String()。比如：undefined和null
* 拼接字符串方式
	* num  +  ""，当 + 两边一个操作数是字符串类型，一个操作数是其它类型的时候，会先把其它类型转换成字符串再进行字符串拼接，返回字符串

#### 转换成布尔类型
* Boolean()
```javascript
console.log(Boolean(-4151));   //true
console.log(Boolean("dsada"));   //true
console.log(Boolean(undefined));   // false
console.log(Boolean(null));   //false
```

### 操作符
运算符  operator ，表达式  组成： 操作数和操作符

#### 算数运算符
```+```（加）、```-```（减）、```*```（乘）、```/```（除）、```%```（取余）
```javascript
var a = 20;   var b = 3;
console.log(a - b); // 17
console.log(a + b); // 23
console.log(a * b); //60
console.log(a / b); //6.666666666666667
console.log(parseInt(a/b)); // 6
console.log(a % b); // 2
```

#### 逻辑运算符(布尔运算符)
```&&```(与) ：两个操作数同时为true，结果为true，否则都是false
```||``` (或) ：两个操作数有一个为true，结果为true，否则为false
```!```  (非) ： 取反
```javascript
console.log(!1); // false
console.log(!0); // true
console.log(true || false); // true
console.log(1 && 0); // 0
```

#### 关系运算符(比较运算符)
```<``` 、```>``` 、 ```>=``` 、 ```<=``` 、 ```==``` 、 ```!=``` 、```===``` (严格等于) 、 ```!==```(严格不等于)
```javascript
//  ==与===的区别：==只进行值得比较，===类型和值同时相等，则相等
console.log(10 == "10");   // true
console.log(10 === "10");   //  false
```

#### 赋值运算符
```=``` 、  ```+=```  、  ```-=```  、  ```*=```  、  ```/=```  、```%=``` 
```javascript
var a = 10;
console.log(a *= a);  // 100
console.log(a /= a);  // 1
console.log(a %= a); // 0
```

#### 一元运算符
一元运算符：只有一个操作数的运算符；5 + 6  两个操作数的运算符 二元运算符.
```++``` ：自身加1；```--```： 自身减1
* 前置 ++：
```javascript
var num1 = 5;
++num1;  // 6
var num2 = 6;
console.log(num1 + ++num2);  // 13
```
* 后置 ++
```javascript
var num1 = 5;
num1++;  // 6
var num2 = 6;
console.log(num1 + num2++);  // 12
```
* 总结
	* 前置++：先加1，后参与运算
	* 后置++：先参与运算，后加1
	* 前置--  ：先减1，后参与运算
	* 后置--  ：先参与运算，后减1

#### 运算符的优先级
优先级从高到底
1. ()  优先级最高
2. 一元运算符  ++   --   !
3. 算数运算符  先*  /  %   后 +   -
4. 关系运算符  >   >=   <   <=
5. 相等运算符   ==   !=    ===    !==
6. 逻辑运算符 先&&   后||
7. 赋值运算符

### 流程控制
一个表达式可以产生一个值，有可能是运算、函数调用、有可能是字面量。表达式可以放在任何需要值的地方。语句可以理解为一个行为，循环语句和判断语句就是典型的语句。一个程序有很多个语句组成，一般情况下;分割一个一个的语句。程序有三种流程基本结构。

#### 顺序结构
默认的，从上到下执行的代码就是顺序结构。

#### 分支结构	
根据不同的情况，执行对应代码。

#### 循环结构
循环结构：重复做一件事情。

### 分支结构

#### if语句

```javascript
// 语法结构
if (/* 条件表达式 */) {
  // 执行语句
}

if (/* 条件表达式 */){
  // 成立执行语句
} else {
  // 否则执行语句
}

if (/* 条件1 */){
  // 成立执行语句
} else if (/* 条件2 */){
  // 成立执行语句
} else if (/* 条件3 */){
  // 成立执行语句
} else {
  // 最后默认执行语句
}
```

#### 三元运算符
```javascript
表达式1 ? 表达式2 : 表达式3 // 是对if……else语句的一种简化写法
// 表达式1成立，执行表达式2；否则，执行表达式3。
var age = parseInt(prompt("请输入您的年龄：")); // prompt 弹出输入框
```

#### switch语句
```javascript
switch (expression) {
  case 常量1:    语句;    break;
  case 常量2:    语句;    break;
  case 常量3:    语句;    break;
...
  case 常量n:    语句;    break;
  default:    语句;    break;
}
```
break 可以省略，如果省略，代码会继续执行下一个 case。
switch 语句在比较值时使用的是全等操作符, 因此不会发生类型转换（例如，字符串'10' 不等于数值 10）
```javascript
var num1 = "10";
switch(num1){
    case 10:    console.log("执行的10");    break;
    case "10":    console.log("执行的\"10\"");    break;
} // 最后执行的是 "case "10""，严格的相等
```

#### 布尔类型的隐式转换
流程控制语句会把后面的值隐式转换成布尔类型
```javascript
// 转换为true   非空字符串  非0数字  true 任何对象
// 转换成false  空字符串  0  false  null  undefined
var a = !!'123';  // true
```

### 循环结构
在javascript中，循环语句有三种，while、do..while、for循环。

#### while语句
```javascript
// 当循环条件为true时，执行循环体，
// 当循环条件为false时，结束循环。
// 计算1-100之间所有数的和
var i = 1;    // 初始化变量，用作循环条件
var sum = 0;  // 存储总和
while (i <= 100) {   // 判断条件
  // 循环体
  sum += i;    //  自增
  i++;    //  结束条件
}
console.log(sum);
```

#### do...while语句
do..while循环和while循环非常像，二者经常可以相互替代，但是do..while的特点是不管条件成不成立，都会执行一次。
```javascript
var i = 1;   // 初始化变量
var sum = 0;
do {
  sum += i;   //   循环体
  i++;   //   自增
} while (i <= 100);   //   循环条件
```

#### for语句
while和do...while一般用来解决无法确认次数的循环。for循环一般在循环次数确定的时候比较方便.
```javascript
// for循环的表达式之间用的是;号分隔的，千万不要写成,
for (初始化表达式1; 判断表达式2; 自增表达式3) {
  // 循环体4

var num1 = 1;    var num2 = 1;    var num3 = 0;
for(var i=3; i<=12;i++){
    num3 = num1 + num2;
    num1 = num2;
    num2 = num3;
} // 斐波拉切数列： 1，1，2，3，5，8，13，21，34，55
    console.log(num3);
```

#### continue和break
***break***：立即跳出整个循环，即循环结束，开始执行循环后面的内容（直接跳到大括号）
***continue***：立即跳出当前循环，继续下一次循环（跳到i++的地方）

#### 调试
* 过去调试JavaScript的方式：alert()   console.log()
* 断点调试：断点调试是指自己在程序的某一行设置一个断点，调试时，程序运行到这一行就会停住，然后你可以一步一步往下调试，调试过程中可以看各个变量当前的值，出错的话，调试到出错的代码行即显示错误，停下。
	* 调试步骤：浏览器中按F12-->sources-->找到需要调试的文件-->在程序的某一行设置断点
	* 调试中的相关操作：
		* Watch: 监视，通过watch可以监视变量的值的变化，非常的常用。
		* F10: 程序单步执行，让程序一行一行的执行，这个时候，观察watch中变量的值的变化。
		* F8：跳到下一个断点处，如果后面没有断点了，则程序执行结束。
* 注意点：监视变量，不要监视表达式，因为监视了表达式，那么这个表达式也会执行。

### 数组
上面学习的数据类型，只能存储一个值(比如：Number/String。想存储多个数据，就用到数组。
所谓数组，就是将多个元素（通常是同一类型）按一定顺序排列放到一个集合中，那么这个集合我们就称之为数组。

#### 数组的定义
数组是一个有序的列表，可以在数组中存放任意的数据，并且数组的长度可以动态的调整。
1. 通过数组字面量创建数组：
```javascript
var arr1 = [];   // 创建一个空数组
var arr2 = [1, 3, 4];    // 创建一个包含3个数值的数组，多个数组项以逗号隔开
var arr3 = ['a', 'c'];    // 创建一个包含2个字符串的数组
console.log(arr3.length);   // 可以通过数组的length属性获取数组的长度
arr3.length = 0;   // 可以设置length属性改变数组中元素的个数
var arr4 = [[0,1,2],[3,4,5]];   //  创建多维数组
```
2. 通过构造函数创建数组：
```javascript
var array = new Array();  //  定义一个空数组 []
var array = new Array(5);  // 定义长度为 5 的空数组，(5) [empty × 5]
var array = new Array(10,20,30,"sad");  //  (4) [10, 20, 30, "sad"]
```

#### 获取数组元素
* 数组的取值
```javascript
// 格式：数组名[下标]	下标又称索引
// 功能：获取数组对应下标的那个值，如果下标不存在，则返回 undefined。
var arr = ['red',, 'green', 'blue'];
arr[0];	  // red
arr[3];   // 这个数组的最大下标为2,因此返回undefined
```
* 遍历数组：遍历：遍及所有，对数组的每一个元素都访问一次就叫遍历。
```javascript
for(var i = 0; i < arr.length; i++) {
	console.log(arr[i]);    // 数组遍历的固定结构
}
```

#### 数组中新增元素
数组的赋值
```javascript
// 格式：数组名[下标/索引] = 值;
// 如果下标有对应的值，会把原来的值覆盖，如果下标不存在，会给数组新增一个元素。
var arr = ["red", "green", "blue"];
arr[0] = "yellow";   // 把red替换成了yellow，arr =  ["yellow", "green", "blue"];
arr[3] = "pink";   // 数组增加一个pink的值，["yellow", "green", "blue","pink"];
```
```javascript
//  冒泡排序
var array = [10, 20, 30, 4, 9, 50];
for (var i = 0; i < array.length - 1; i++) {     // 比较的轮数
    for (var j = 0; j < array.length - 1 - i; j++) {   // 每轮比较的次数
        if (array[j] > array[j + 1]) {    // 从小到大排序；从大到小排序就是 <
            var temp = array[j];
            array[j] = array[j + 1];
            array[j + 1] = temp;
        }
    }
}
console.log(array);   //  [4,9,10,20,30,50]
```

### 函数
把一段相对独立的具有特定功能的代码块封装起来，形成一个独立实体，就是函数，起个名字（函数名），在后续开发中可以反复调用。函数的作用就是封装一段代码，将来可以重复使用。

* 函数声明：```function 函数名(){ // 函数体 }```
* 函数表达式：```var fn = function() {  // 函数体 }```
* 特点：函数声明的时候，函数体并不会执行，只要当函数被调用的时候才会执行。函数一般都用来干一件事情，需用使用动词+名词命名，表示做一件事情 `tellStory` `sayHello`等。

#### 函数的调用
* 调用函数的语法：```函数名();```
* 特点：函数体只有在调用的时候才会执行，调用需要()进行调用。可以调用多次(重复使用)
```javascript
function getSum() {   // 求1-100之间所有数的和
    var sum = 0;
    for (var  i = 0; i < 100; i++) {
       sum += i;
     }
     console.log(sum);
}
getSum();   // 调用
```

#### 函数的参数
```javascript
// 函数内部是一个封闭的环境，可以通过参数的方式，把外部的值传递给函数内部
// 带参数的函数声明
function 函数名(形参1, 形参2, 形参...){
  // 函数体
}
// 带参数的函数调用
函数名(实参1, 实参2, 实参3);
```
形参和实参：
* 形式参数：在声明一个函数的时候，为了函数的功能更加灵活，有些值是固定不了的，对于这些固定不了的值。我们可以给函数设置参数。这个参数没有具体的值，仅仅起到一个占位置的作用，我们通常称之为形式参数，也叫形参。
* 实际参数：如果函数在声明时，设置了形参，那么在函数调用的时候就需要传入对应的参数，我们把传入的参数叫做实际参数，也叫实参。
```javascript
var x = 5, y = 6;
fn(x,y); 
function fn(a, b) {
  console.log(a + b);
}
//x,y实参，有具体的值。函数执行的时候会把x,y复制一份给函数内部的a和b，函数内部的值是复制的新值，无法修改外部的x,y
```

#### 函数的返回值
当函数执行完的时候，并不是所有时候都要把结果打印。我们期望函数给我一些反馈（比如计算的结果返回进行后续的运算），这个时候可以让函数返回一些东西。也就是返回值。函数通过return返回一个返回值
```javascript
//声明一个带返回值的函数
function 函数名(形参1, 形参2, 形参...){
  //函数体
  return 返回值;
}
//可以通过变量来接收这个返回值
var 变量 = 函数名(实参1, 实参2, 实参3);
```
函数的调用结果就是返回值，因此我们可以直接对函数调用结果进行操作。
* 如果函数没有显示的使用 return语句 ，那么函数有默认的返回值：undefined
* 如果函数使用 return语句，那么跟再return后面的值，就成了函数的返回值
* 如果函数使用 return语句，但是return后面没有任何值，那么函数的返回值也是：undefined
* 函数使用return语句后，这个函数会在执行完 return 语句之后停止并立即退出，也就是说return后面的所有其他代码都不会再执行。

#### arguments 的使用
JavaScript中，arguments对象是比较特别的一个对象，实际上是当前函数的一个内置属性。也就是说所有函数都内置了一个arguments对象，arguments对象中存储了传递的所有的实参。arguments是一个伪数组，因此及可以进行遍历
```javascript
function f(){
    //Arguments [Array(6), callee: ƒ, Symbol(Symbol.iterator): ƒ]
    console.log(arguments); 
    console.log(arguments[0]); // (6) [1, 85, 8, 3, 4, 0]
    console.log(arguments[1]); // undefined
    console.log(arguments.length); // 1
}
f([1,85,8,3,4,0]);
```

#### 函数其它
1. ***匿名函数***
匿名函数：没有名字的函数。
匿名函数自调用匿名函数如何使用：```将匿名函数赋值给一个变量，这样就可以通过变量进行调用。```
```javascript
var f1 = function (){    
   //   函数体   
};   //  要有逗号结尾
f1();    //  调用函数
```
关于自执行函数（匿名函数自调用）的作用：防止全局变量污染。

2. ***自调用函数***
匿名函数不能通过直接调用来执行，因此可以通过匿名函数的自调用的方式来执行
```javascript
(function () {
  alert(123);
})();   //  弹出提示框，123
```
3. ***函数是一种数据类型***
```javascript
function fn() {}
console.log(typeof fn);   //  function
```
* 函数作为参数：因为函数也是一种类型，可以把函数作为两一个函数的参数，在两一个函数中调用
* 函数做为返回值：因为函数是一种类型，所以可以把函数可以作为返回值从函数内部返回。
```javascript
function fn(b) {
  var a = 10;
  return function () {   alert(a+b);   }
}
fn(15)();   //  弹出对话框，显示 25
```

### 作用域
作用域：变量可以起作用的范围

#### 全局变量和局部变量
* 全局变量：在任何地方都可以访问到的变量就是全局变量，对应全局作用域
* 局部变量：只在固定的代码片段内可访问到的变量，最常见的例如函数内部。对应局部作用域(函数作用域)
	* 不使用var声明的变量是全局变量，不推荐使用。
	* 变量退出作用域之后会销毁，全局变量关闭网页或浏览器才会销毁

#### 块级作用域
任何一对花括号（｛和｝）中的语句集都属于一个块，在这之中定义的所有变量在代码块外都是不可见的，我们称之为块级作用域。
**在 ES5 之前没有块级作用域的的概念,只有函数作用域**，现阶段可以认为JavaScript没有块级作用域

#### 词法作用域
变量的作用域是在定义时决定而不是执行时决定，也就是说词法作用域取决于源码，通过静态分析就能确定，因此词法作用域也叫做静态作用域。

**在 js 中词法作用域规则:**
* 函数允许访问函数外的数据.
* 整个代码结构中只有函数可以限定作用域.
* 作用域规则首先使用提升规则分析
* 如果当前作用规则中有名字了, 就不考虑外面的名字
```javascript
var num = 123;
function foo() {
  console.log( num ); // 123
}
foo();

if ( false ) {
    var num = 123;
}
console.log( num ); // undefiend，如果 false 改为 true，则为123

function f2(){
     num = 10;
}
//        f2();
console.log(num);
// 调用了 f2() 就是输出 10，相当于开辟了空间；没有调用就报错
```

#### 作用域链
只有函数可以制造作用域结构， 那么只要是代码，就至少有一个作用域, 即全局作用域。凡是代码中有函数，那么这个函数就构成另一个作用域。如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域。
将这样的所有的作用域列出来，可以有一个结构: 函数内指向函数外的链式结构。就称作作用域链。
```javascript
// 案例1：
function f1() {
    function f2() {
    }
}

var num = 456;
function f3() {
    function f4() {    
    }
}
```

![作用域链1](./images/06-1.png)
```javascript
// 案例2
function f1() {
    var num = 123;
    function f2() {
        console.log( num );
    }
    f2();
}
var num = 456;
f1();
```

![作用域链2](./images/06-2.png)

### 预解析
JavaScript 代码的执行是由浏览器中的 JavaScript 解析器来执行的。
JavaScrip t解析器执行 JavaScript 代码的时候，分为两个过程：预解析过程和代码执行过程。

* 预解析过程：
	* 把变量的声明提升到当前作用域的最前面，只会提升声明，不会提升赋值。
	* 把函数的声明提升到当前作用域的最前面，只会提升声明，不会提升调用。
	* 先提升var，再提升function
```javascript
var a = 25;
console.log(a); // 25
function a() {
    console.log(a); // undefine
    var a = 10;
}
 a(); // a is not a function

var a;
console.log(a);  // ƒ a() {   console.log('aaaaa'); }
function a() {
    console.log('aaaaa');
 }
 a();   //   aaaaa
 var a = 1;
console.log(a); // 1
```

#### 全局解析规则
**函数内部解析规则**
* ***变量提升***：定义变量的时候，变量的声明会被提升到作用域的最上面，变量的赋值不会提升。
* ***函数提升***：JavaScript解析器首先会把当前作用域的函数声明提前到整个作用域的最前面
```javascript
// 1、-----------------------------------
var num = 10;
fun();
function fun() {
    console.log(num);  // undefined
    var num = 20;
}
//2、-----------------------------------
var a = 18;
f1();
function f1() {
    var b = 9;
    console.log(a);  // undefined
    console.log(b);  // 9
    var a = '123';
}
// 3、-----------------------------------
f1();
console.log(c);  //  9
console.log(b);  //  9
console.log(a);  //   报错
function f1() {
    var a = b = c = 9;  //  等价于  var a; a=9; b=9; c=9;
    console.log(a);  //  9
    console.log(b);  //  9
    console.log(c);  //  9
}
```

### 对象
现实生活中：万物皆对象，对象是一个具体的事物，一个具体的事物就会有行为和特征。
JavaScript中的对象：
* JavaScript中的对象其实就是生活中对象的一个抽象
* JavaScript的对象是无序属性的集合。
	* 其属性可以包含基本值、对象或函数。对象就是一组没有顺序的值。我们可以把JavaScript中的对象想象成键值对，其中值可以是数据和函数。
	* 对象的行为和特征：
		* 特征---属性，事物的特征在对象中用属性来表示。
		* 行为---方法，事物的行为在对象中用方法来表示。

#### 对象创建方式
1. 对象字面量
```javascript
var o = {
    name: 'cjr',
    age: 18,
    sex: male,
    sayHi: function () {
      console.log(this.name);
    }
}; 
```
2. new Object()创建对象
```javascript
var person = new Object();    //   也可以使用 var person = {};  类似数组  var a=[];
person.name = 'cjr';
person.age = 25;
person.job = 'IT';
person.sayHi = function(){
    console.log('Hello,everyBody');
}
```
3. 工厂函数创建对象
```javascript
function Dog(name,age){
    var dog = new Object();
    dog.name = name;
    dog.age = age;
    dog.bark = function(){
        console.log("呜呜呜呜呜~~~");
    };
    return dog;
}
var ahuang = Dog("阿黄", 3);
console.log(ahuang);  // {name: "阿黄", age: 3, bark: ƒ}
ahuang.bark();   // 呜呜呜呜呜~~~
```
4. 自定义构造函数
```javascript
function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayHi = function(){
        console.log('Hello,everyBody');
    }
}
var p1 = new Person('张三', 22, 'actor');
p1.sayHi(); //  Hello,everyBody
console.log(p1 instanceof Person); // true，p1 是不是 Person 对象
```
* 属性和方法
	* 如果一个变量属于一个对象所有，那么该变量就可以称之为该对象的一个属性，属性一般是名词，用来描述事物的特征。
	* 如果一个函数属于一个对象所有，那么该函数就可以称之为该对象的一个方法，方法是动词，描述事物的行为和功能

#### new 关键字
构造函数 ，是一种特殊的函数。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。
1. 构造函数用于创建一类对象，首字母要大写。如，Person
2. 构造函数要和 new 一起使用才有意义。如 var zhangsan = new Person();
3. new在执行时会做四件事情：
	1. new会在内存中开辟空间，存储创建一个新的空对象
	2. new 会让 this 指向这个新的对象
	3. 执行构造函数  目的：给这个新对象加属性和方法
	4. new 会返回这个新对象

#### this 详解
JavaScript中的this指向问题：
```javascript
	1. 函数在定义的时候 this 是不确定的，只有在调用的时候才可以确定
	2. 一般函数直接执行，内部 this 指向全局 window
	3. 函数作为一个对象的方法，被该对象所调用，那么 this 指向的是该对象
	4. 构造函数中的 this 其实是一个隐式对象，类似一个初始化的模型，所有方法和属性都挂载到了这个隐式对象身上，后续通过 new 关键字来调用，从而实现实例化
```

#### 对象的使用
1. ***遍历对象的属性***：通过for..in语法可以遍历一个对象
```javascript
var obj = {};
for (var i = 0; i < 10; i++) {
    obj[i] = i * 2;
}   //  obj[key]  直接调用，两种方式都可以，但是没有属性的时候用这个
for(var key in obj) {
    console.log(key + "==" + obj[key]);  //  key 是 obj 的键
}   //  obj.key 如果有 key 就是调用，没有就是创建
```
2. ***删除对象的属性***
```javascript
function fun() { 
    this.name = 'bob';
}
var obj = new fun(); 
console.log(obj.name);   //   bob 
delete obj.name;
console.log(obj.name);   //  undefined
```

### 简单类型和复杂类型的区别
* 原始数据类型：Number，String，Boolean，Null，Undefined，Object
	* 基本类型又叫做值类型：number，string，boolean ；简单数据类型，基本数据类型，在存储时，变量中存储的是值本身，因此叫做值类型。栈 中存储
	* 复杂类型又叫做引用类型：object ；复杂数据类型，在存储是，变量中存储的仅仅是地址（引用），因此叫做引用数据类型。栈和堆 中存储
	* 空类型：undefined，null
* 堆和栈
	* 栈（操作系统）：由操作系统自动分配释放 ，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈；
	* 堆（操作系统）： 存储复杂类型(对象)，一般由程序员分配释放， 若程序员不释放，由垃圾回收机制回收，分配方式倒是类似于链表。
	* 注意：JavaScript中没有堆和栈的概念，此处用堆和栈来讲解，目的方便理解和方便以后的学习。
	* 
![基本类型在内存中的存储](./images/1498288494687.png)

![复杂类型在内存中的存储](./images/1498700592589.png)

![基本类型作为函数的参数](./images/1497497605587-8288640195.png)

![复杂类型作为函数的参数](./images/1497497865969.png)
```javascript
function Person(name,age,salary) {
    this.name = name;
    this.age = age;
    this.salary = salary;
}
function f1(person) {
    person.name = "cccc";
    person = new Person("aaaa",18,10);   //  此时 person 存储的不是 p 的地址了，是新的地址
}
var p = new Person("bbbb",18,1000);
console.log(p.name);  //  bbbb
f1(p);
console.log(p.name);  //  cccc
```

### JSON
JSON(JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。它基于 ECMAScript (欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

#### JSON 语法规则
任何支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。但是对象和数组是比较特殊且常用的两种类型：
* 对象表示为键值对，花括号保存对象
* 数据由逗号分隔，方括号保存数组

***JSON 键/值对***
JSON 键值对是用来保存 JS 对象的一种方式，和 JS 对象的写法也大同小异，键/值对组合中的键名写在前面并用双引号 "" 包裹，使用冒号 : 分隔，然后紧接着值：
```{"firstName": "Json"}```
等价于这条 JavaScript 语句：```{firstName : "Json"}```

#### JSON 与 JS 对象的关系
JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。
```javascript
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
```
JSON 和 JS 对象互转：
* 对象转换为 JSON 字符串，使用 JSON.stringify() 方法：
	* ```var json = JSON.stringify({a: 'Hello', b: 'World'}); //结果是 '{"a": "Hello", "b": "World"}'```
* 从 JSON 转换为对象，使用 JSON.parse() 方法：
	* ```var obj = JSON.parse('{"a": "Hello", "b": "World"}'); //结果是 {a: 'Hello', b: 'World'}```

### 内置对象
JavaScript中的对象分为3种：内置对象、浏览器对象(web api)、自定义对象
JavaScript 提供多个内置对象：Math/Array/Number/String/Boolean...
对象只是带有**属性**和**方法**的特殊数据类型。
可以通过 [MDN](https://developer.mozilla.org/zh-CN/) 查看。

#### Math 对象
Math对象不是构造函数，它具有数学常数和函数的属性和方法，都是以静态成员的方式提供。跟数学相关的运算来找Math中的成员（求绝对值，取整）
```javascript
console.log(Math.PI); // 3.141592653589793
console.log(Math.abs(null)); // 0
console.log(Math.abs(undefined)); // NaN
console.log(Math.ceil(10.33);) // 11
Math.floor(10.9999);  //  10
Math.max(10,20,3,50,-12); // 50
Math.min(10,-5,60,20); // -5
Math.pow(2,3);  // 8
Math.fround(1.36498);   //   1.3649799823760986
Math.random();  //  伪随机数在范围 [0，1)，包括0，但是不包括1。
Math.round(20.5514654);  //  21
Math.sign(-256);   //   -1
Math.sqrt(9);  // 3
```

#### Date 对象
Date 对象基于1970年1月1日（世界标准时间）起的毫秒数。
```javascript
var utcDate1 = new Date(Date.UTC(96, 1, 2, 3, 4, 5));
console.log(utcDate1.toUTCString());  //  Fri, 02 Feb 1996 03:04:05 GMT
Date.now();  // 1547013241828
Date.parse('01 Jan 1970 00:00:00 GMT');  //  0
var birthday = new Date('August 19, 1975 23:15:30');
birthday.getDate(); // 19
birthday.getDay(); // 2   一周的第几天，0 表示星期天。
birthday.getFullYear(); // 1975
birthday.getHours();  // 23
birthday.getMinutes();  // 15
birthday.getMonth();  // 7返回指定的日期对象的月份，0表示一月
birthday.getSeconds();  // 30
birthday.getTime();  // 177693330000,返回一个时间的格林威治时间数值。
birthday.toDateString();  //  "Tue Aug 19 1975"
birthday.toString(); //  "Tue Aug 19 1975 23:15:30 GMT+0800 (中国标准时间)"
birthday.toJSON(); // "1975-08-19T15:15:30.000Z"
birthday.toLocaleDateString();  // "1975/8/19"
```

#### String 对象
String 全局对象是一个用于字符串或一个字符序列的构造函数。
```javascript
var x = "Mozilla";
x.length;  //  7
x.charAt(1);  // o
x.charCodeAt(1);  //  111,字符的 UTF-16 代码单元值的数字
x.codePointAt(1);  //  111 返回 一个 Unicode 编码点值的非负整数。
x.concat(",Hello ","world!");  // "Mozilla,Hello world!"
x.endsWith("lla");  // true
x.indexOf("o");  // 1
x.lastIndexOf("l");  // 5 返回指定值在字符串中最后出现的位置,0开始\
x.match(/[a-lA-L]/gi);  //  (4) ["i", "l", "l", "a"]
x.search(/[a-lA-L]/gi);  // 3 第一次出现的索引
x.repeat(3);  // "MozillaMozillaMozilla"
x.replace(/[a-lA-L]/gi, "???");  //  "Moz????????????"
x.slice(2,4);  //  "zi"
x.split("");  //  (7) ["M", "o", "z", "i", "l", "l", "a"]
x.startsWith("M");  // true
x.substring(3,0);  //  "Moz"
x.toLocaleLowerCase();  // "mozilla"
x.toLocaleUpperCase();  //  "MOZILLA"
x.toLowerCase();  //   "mozilla"
x.toUpperCase();  //    "MOZILLA"
var y = " w h a t  ";
y.trim();   // "w h a t"
y.trimLeft();  //  "w h a t  "
y.trimRight();   //  " w h a t"
var z = new String("mozilla");   typeof z;  //  "object"
typeof z.indexOf();   //  "number"
z.indexOf("i");  //  3
"aacsac".localeCompare("bbdasd");  // -1
"bbasdas".localeCompare("aacvadsfa");  // 1
String.fromCharCode(0x404); // "Є" 返回Unicode值序列创建的字符串。
String.fromCodePoint(0x404);  // "\u0404" 使用 Unicode 编码创建的字符串。
```

#### Array 对象
JavaScript 的 Array 对象是用于构造数组的全局对象，数组类似与列表的高阶对象。
```javascript
var fruits = ['Apple', 'Banana'];
fruits.length;  // 2
Array.from(fruits);  //   (2) ["Apple", "Banana"]
Array.isArray(fruits);   // true
Array.of(7);   //  [7]
Array(7);   //   (7) [empty × 7]
fruits.concat("Strawberry");  //  (3) ["Apple", "Banana", "Strawberry"]
var array1 = [1, 2, 3, 4];
console.log(array1.fill(0, 2, 4));  //  [1, 2, 0, 0]
var filtered = [12, 5, 8, 130, 44].filter(function (element) {
  return element >= 10;
});   //   (3) [12, 130, 44]
fruits.find(function (e){ return e == "Banana";});  // "Banana"
fruits.findIndex(function (e){ return e == "Banana";});  // 1
fruits.forEach(function(e){ console.log(e);});  // Apple     Banana
fruits.includes("Banana");   //  true
fruits.indexOf("Banana");   //  1
fruits.keys();    //   Array Iterator {}
for(let key of fruits.keys()){ console.log(key);};   // 0  1
fruits.map(function(e) { return e + "Pen";});    //   (2) ["ApplePen", "BananaPen"]
fruits.pop();   //    "Banana"
fruits.push("Banana","Strawberry");   // (3) ["Apple", "Banana", "Strawberry"]
[0, 1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array){
  return accumulator + currentValue;
});    //    0 + 1 + 2 + 3 + 4   10
fruits.reverse();    //   (3) ["Strawberry", "Banana", "Apple"]
fruits.shift();   //   "Strawberry"
fruits.unshift("Strawberry");   // 3    (3) ["Strawberry", "Banana", "Apple"]
fruits.slice(0,2);   //   (2) ["Strawberry", "Banana"]
fruits.sort(function (a,b){ return a>b;});   //  (3) ["Apple", "Banana", "Strawberry"]
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');   //   ['Jan', 'Feb', 'March', 'April', 'June']
months.splice(4, 1, 'May');   //    ['Jan', 'Feb', 'March', 'April', 'May']
``` 