# javascript

## javascript 基础

1.常见的 HTML 事件
```
onchange    HTML 元素已被改变
onclick 用户点击了 HTML 元素
onmouseover 用户把鼠标移动到 HTML 元素上
onmouseout  用户把鼠标移开 HTML 元素
onkeydown   用户按下键盘按键
onload  浏览器已经完成页面加载
```

2.数值转换
```
var x = 9.656;  // 默认保留小数点后3位
x.toExponential(2);     // 返回 9.66e+0
x.toExponential(4);     // 返回 9.6560e+0
x.toExponential(6);     // 返回 9.656000e+0

var x = 9.656;
x.toFixed(0);           // 返回 10
x.toFixed(2);           // 返回 9.66
x.toFixed(4);           // 返回 9.6560
x.toFixed(6);           // 返回 9.656000
// toFixed方法可以使用9.66e+10，含有e的

var x = 9.656;          // 返回指定长度数
x.toPrecision();        // 返回 9.656
x.toPrecision(2);       // 返回 9.7，会四舍五入
x.toPrecision(4);       // 返回 9.656
x.toPrecision(6);       // 返回 9.65600

x = new Date();
Number(x);        // 返回 1560151028844
x = "10 20"
Number(x);        // 返回 NaN
parseInt("10.33");      // 返回 10
parseInt("10 20 30");   // 返回 10
parseFloat("10.33");     // 返回 10.33
parseFloat("10 20 30");  // 返回 10
```

3.数组
```
var person = [];
person[0] = "Bill";
person[1] = "Gates";
person[2] = 62;
var x = person.length;          // person.length 返回 3
var y = person[0];              // person[0] 返回 "Bill"
// person 返回 [firstName: "Bill", lastName: "Gates", age: 62]
// person["firstName"] 返回 "Bill"

Math.max(1,2,3,0,10)
Math.max.apply(null,[1,4,3,99,5]);//99
// Math.max.apply(null, [1, 2, 3]) 等于 Math.max(1, 2, 3) 
// Math.max.apply(Math.max, [1, 2, 3])   // 3
// Math.max.apply(this, [1, 2, 3])  // 3
// Math.max.apply(Math, [1, 2, 3])  // 3
// Math.max.apply([1, 2, 3])    // -Infinity

var arr1=[1,2];
var arr2=[3,4,5];
arr1.push(arr2);//[1,2,[3,4,5]]
Array.prototype.push.apply(arr1,arr2);//5
//arr1输出为[1,2,3,4,5]

obj1.(method).call(obj2,argument1,argument2);
// call的作用就是把obj1的方法放到obj2上使用，后面的argument1..这些做为参数传入。
function add (x, y) 
{ 
    console.log (x + y);
} 
function minus (x, y) 
{ 
    console.log (x - y); 
} 
add.call (minus , 1, 1);    // 2  等价于 add(1,1) 
```

[参考文章：call与apply 之 借刀杀人](https://zhuanlan.zhihu.com/p/32116251)

4.类型
```
typeof "Bill"                 // 返回 "string"
typeof 3.14                   // 返回 "number"
typeof NaN                    // 返回 "number"
typeof false                  // 返回 "boolean"
typeof [1,2,3,4]              // 返回 "object"
typeof {name:'Bill', age:62}  // 返回 "object"
typeof new Date()             // 返回 "object"
typeof function () {}         // 返回 "function"
typeof myCar                  // 返回 "undefined" *
typeof null                   // 返回 "object"

"Bill".constructor                // 返回 "function String() { [native code] }"
(3.14).constructor                // 返回 "function Number() { [native code] }"
false.constructor                 // 返回 "function Boolean(){ [native code] }"
[1,2,3,4].constructor             // 返回 "function Array()  { [native code] }"
{name:'Bill', age:62}.constructor // 返回 "function Object() { [native code] }"
new Date().constructor            // 返回 "function Date()   { [native code] }"
function () {}.constructor        // 返回 "function Function(){ [native code] }"
```

5.异常处理
```
// try 语句使您能够测试代码块中的错误。
// catch 语句允许您处理错误。
// throw 语句允许您创建自定义错误。
// finally 使您能够执行代码，在 try 和 catch 之后，无论结果如何。

x = document.getElementById("input").value;
try { 
    if(x == "") throw "空的";
    if(isNaN(x)) throw "不是数字";
    x = Number(x);
    if(x < 5) throw  "太小";
    if(x > 10) throw "太大";
}
catch(err) {
    message.innerHTML = "输入是 " + err;
}
finally {
    document.getElementById("input").value = "";
}
```
Error 对象提供两个有用的属性：name 和 message。
error 的 name 属性可返回六个不同的值，err.name：
-  EvalError   已在 eval() 函数中发生的错误，新版使用 SyntaxError 代替
-  RangeError  已发生超出数字范围的错误
-  ReferenceError  已发生非法引用
-  SyntaxError 已发生语法错误
-  TypeError   已发生类型错误
-  URIError    在 encodeURI() 中已发生的错误

6.let 和 const 
（1）用 let 或 const 声明的变量和常量不会被提升！

（2）严格模式
```
"use strict";
x = 3.14;       // 这会引发错误，因为 x 尚未声明

"use strict";
var x = 3.14;
delete x;                // 这将引发错误

"use strict";
function x(p1, p2) {}; 
delete x;                 // 这将引发错误
```

（3）let
```
{ 
  let x = 10;  // 使用 let 关键词声明拥有块作用域的变量，var 是全局的
}

var x = 10;
{ 
  let x = 6;  // 此处 x 为 6
}
// 此处 x 为 10

let i = 7;
for (let i = 0; i < 10; i++) {  }
// 此处 i 为 7

let carName = "porsche";
// 此处的代码不可使用 window.carName

var x = 10;       // 允许
let x = 6;       // 不允许
{
  var x = 10;   // 允许
  let x = 6;   // 不允许
}
```

（4）const
```
const PI = 3.141592653589793;
PI = 3.14;      // 会出错，const 不能重新赋值
PI = PI + 10;   // 也会出错

var x = 10; // 此处，x 为 10
{ 
  const x = 6;   // 此处，x 为 6
}
// 此处，x 为 10

const PI;
PI = 3.14159265359;  // 不正确
const PI = 3.14159265359;  // 正确

// 您可以创建 const 对象：
const car = {type:"porsche", model:"911", color:"Black"};
car.color = "White";  // 您可以更改属性：
car.owner = "Bill";  // 您可以添加属性：

// 您可以创建常量数组：
const cars = ["Audi", "BMW", "porsche"];
cars[0] = "Honda";  // 您可以更改元素：
cars.push("Volvo");  // 您可以添加元素：
```


7.this：this 关键词指的是它所属的对象。
```
// fullName : function() {  return this.firstName + " " + this.lastName;}
在方法中，this 指的是所有者对象。

// var x = this;  [object Window]
单独的情况下，this 指的是全局对象。

// function myFunction() {  return this; }  [object Window]
在函数中，this 指的是全局对象。 

// "use strict"; function myFunction() { return this; }  undefined
在函数中，严格模式下，this 是 undefined。

// <button onclick="this.style.display='none'">  点击！ </button>
在事件中，this 指的是接收事件的元素。

var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var person2 = {
  firstName:"Bill",
  lastName: "Gates",
}
person1.fullName.call(person2);  // 会返回 "Bill Gates"
call() 和 apply() 这样的方法可以将 this 引用到任何对象
```

