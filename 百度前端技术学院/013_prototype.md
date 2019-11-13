# javascript

## 原型

1.构造函数，实例对象，原型对象
（1）构造函数是用来在创建对象时初始化对象，即为对象成员变量赋初始值
（2）实例对象是构造函数的具体实现，用new创建的
（3）原型对象是prototype

2.注意点
（1）修改原型对象之后需要设置构造器的指向，如果不设置，会指向Object
```
Student.prototype = {
    constructor: Student,
    eat: function(){ console.log("eat"); }
}
```
（2）需要先设置原型对象，再创建对象（实例化），才可以访问原型中的方法

3.继承
（1）原型继承，缺点，无法设置构造函数的参数，只调用一次
```
    function Person() {
        this.name = "张三";
        this.age = 23;
    }
    function Student() {
        this.score = 100;
    }
    Student.prototype = new Person();
    Student.prototype.constructor = Student;
    var s1 = new Student();
    console.dir(s1);
    console.log(s1.constructor);
```

（2）bind方法，改变函数的this，并返回一个新的函数（不调用函数）
call方法，改变函数中的this，直接调用函数
apply方法，Math.max.apply(null, [1,2,3,4]);
```
    function getMax(a, b) {
        console.log(this);
        console.log(a > b ? a : b);
    }
    var obj = { name: "zhangsan" };

//  getMax(1,2);  // window
//  var f = getMax.bind(obj, 2, 3);
//  f();

    getMax.call(obj,4,5);
```

(3)构造函数继承，但是原型中的方法还不能继承，如Person.prototype.sayHi...
```
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    function Student(name,age,score) {
        this.score = score;
        Person.call(this,name,age);
    }
    var s1 = new Student("张三", 18, 100);
    console.log(s1);
```

（4）组合继承
```
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.sayHi = function () {
        console.log("hi");
    };
    function Teacher(name, age, sex) {
        Person.call(this, name, age);
        this.sex = sex;
    }
    Teacher.prototype = new Person(); // 目的：为了继承父类方法
//    Teacher.prototype = Person.prototype; // 这个会让父类也会有该方法
    Teacher.prototype.teach = function () {
        console.log("teach");
    };
    Teacher.prototype.constructor = Teacher;
    var t1 = new Teacher("zhangsan", 12, "male");
    console.dir(t1);
```

4.this：函数内部的this，是由函数调用的时候来确定其指向的

5.函数
（1）函数中有四个属性，arguments、caller、name、length
（2）arguments 是函数传入的参数
（3）caller 是函数的调用者
（4）name 函数的名称
（5）length 函数形参的个数

6.闭包：是使用被作用域封闭的变量，函数，闭包等执行的一个函数的作用域。通常我们用和其相应的函数来指代这些作用于。（可以访问独立数据的函数）
```
    var lis = document.getElementsByTagName("li");
    for(var i = 0, len = lis.length; i < len; i++){
        var li = lis[i];
        (function (i) {
            li.onclick = function () {
              console.log(i); // 内部函数访问到外部函数的变量
            };
        })(i);
    }
```

（1）闭包案例
```
    var name = "Win";
    var obj = {
        name: "obj",
        getName: function () {
            return function () {
                return this.name;
            }
        }
    };
    console.log(obj.getName()()); // "win"

    var name = "win_name";
    var obj = {
        name: "obj",
        getName: function () {
            var that = this;
            return function () {
                return that.name;
            }
        }
    };
    console.log(obj.getName()());  // "obj"
```

（2）“执行栈”中存储由上向下执行，当执行到有回掉函数的，会把它放到“任务队列"中，跳过执行后面代码。把”执行栈“中的代码执行完毕之后，会有”消息循环“依次循环执行”任务队列“中的函数，每循环一次执行一次。
```
    console.log("start");
    for(var i =0; i < 3;i++){
//        setTimeout(function () {
//            console.log(i);
//        },0);
        (function (i) {
            setTimeout(function () {
                console.log(i);
            },0);
        })(i);
    }
    console.log("end");
-------------------------------- 执行结果
start
end
0
1
2
```

7.递归
```
    function fn(n) {
        if(n === 1){
            return 1;
        }
        return n + fn(n - 1);
    }
    console.log(fn(5));
```

8.拷贝：浅拷贝、深拷贝
（1）浅拷贝，只复制第一层，对象里面原来的对象和复制的对象都指向同一对象
```
    var obj1 = {
        name: "zs",
        age: 10,
        sex: "male",
        say: {   n: "123",   b: "123"   }
    };
    var obj2 = {};
    for (var key in obj1) {
        obj2[key] = obj1[key];
    }
    obj1.name = "ls";  // 不会改变obj2中的值
    obj1.say.n = "234";  // 会改变obj2中的值
    console.log(obj1);
    console.log(obj2);
```

（2）深拷贝
```
    function deepCopy(obj1, obj2) {
        for (var key in obj1) {
            if (obj1[key] instanceof Object) {
                obj2[key] = {};
                deepCopy(obj1[key], obj2[key]);
            } else if (obj1[key] instanceof Array) {
                obj2[key] = [];
                deepCopy(obj1[key], obj2[key]);
            } else {
                obj2[key] = obj1[key];
            }
        }
    }
    var o1 = {name: "zs", age: 123, oo: {a: 123, b: 213}};
    var o2 = {};
    deepCopy(o1, o2);
    o1.name = "sda";
    o1.oo.a = 12321;
    console.log(o1);
    console.log(o2);
```

9.正则表达式
（1）正则表达式有exec和test的方式，以及String的match、replace、search和split方法。
```
    var str = "张三:2500,李四:3000,王五:5000";
    var reg =/\d+/g;
    var arr = reg.exec(str);
    console.log(arr); // 2500
    arr = reg.exec(str);
    console.log(arr); // 3000
    arr = reg.exec(str);
    console.log(arr); // 5000
    arr = reg.exec(str);
    console.log(arr); // null

    var regStr = new RegExp('\\d','g');
    console.log(regStr.test(str)); // true

    var tag = "<title>aaaaaaaaa</title> <span> bbbb</span></title>";
    var arr = tag.match(/^<title>.+?<\/title>/gi);
    console.log(arr); // ["<title>aaaaaaaaa</title>"]

    var newArr = tag.replace(/<.+?>/gi,'');
    console.log(newArr); // aaaaaaaaa  bbbb

    var splitArr = tag.split(/<.+?>/gi);
    console.log(splitArr); // ["", "aaaaaaaaa", " ", " bbbb", "", ""]

    var searchArr = tag.search(/<.+?>/gi);
    console.log(searchArr); // 0 返回匹配到的索引
```
(2)匹配规则
-  \d：匹配数字； \D：匹配任意非数字的字符
-  \w：匹配字母或数字或下划线； \W：匹配任意不是字母，数字，下划线
-  \s：匹配任意的空白符； \S：匹配任意不是空白符的字符
-  .：匹配除换行符以外的任意单个字符
-  ^：表示匹配行首的文本； $：表示匹配行尾的文本

## 变量

1.原始类型（String、Number、Boolean、Undefined、Null、Symbol）、复杂类型（Object（Array...））
```
var y = 123e5;      // 12300000
var z = 123e-5;     // 0.00123

typeof undefined              // undefined
typeof null                   // object
null === undefined            // false
null == undefined             // true
```

2.Number、Math
```
Math.PI              // 3.141592653589793
Math.abs(-10.1)      // 10.1
Math.ceil(12.1)      // 13
Math.floor(12.6)     // 12
Math.round(2.5)      // 3
Math.min(12,3,-1,0)  // -1
Math.max(12,3,-1,0)  // 12
Math.pow(2,3)        // 8
Math.random()        // 0.6744405581379245

var a = 123;
a.toExponential(3);  // 1.230e+2   
a.toFixed(2);        // 123.00
a.toPrecision(1);    // "1e+2"
a.toPrecision(5);    // "123.00"

Number.MAX_VALUE     // 1.7976931348623157e+308
Number.MIN_VALUE     // 5e-324
Number.NEGATIVE_INFINITY  // -Infinity
Number.POSITIVE_INFINITY  // Infinity
Number.NaN           // NaN
```

3.String
```
var txt="Hello world!";
txt.length;                   // 12
txt.toLocaleUpperCase();      // "HELLO WORLD!"
txt.toLocaleLowerCase();      // "hello world!"
txt.charAt(1);                // "e"
txt.charCodeAt(1);            // 101
txt.indexOf("e");             // 1
txt.lastIndexOf("l");         // 9
txt.slice(0,4);               // "Hell"
txt.slice(0,-3);              // "Hello wor"，-3会被转为12+(-3)=9
txt.slice(0,9);               // 
txt.substr(0,4);              // "Hell"
txt.substr(0,-3);             // ""，-3会被转为0
txt.substr(0,0);              // ""
txt.match(/o/g);              // ["o", "o"]
txt.replace(/o/g,"Q");        // "HellQ wQrld!"
txt.search(/o/g);             // 4

var result = ("Hello ").concat("world!");  // "Hello world!"
```

4、Array
```
Array.from("foo");               // ["f", "o", "o"]
Array.isArray([1, 2, 3]);        // true
Array.of(7);                     // [7]，Array(7) => [ , , , , , , ]

var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];
array1.concat(array2);           // ["a", "b", "c", "d", "e", "f"]

function isBigEnough(element, index, array) {
  return element >= 10;
}
[12, 5, 8, 130, 44].every(isBigEnough);   // false
[12, 54, 18, 130, 44].every(isBigEnough); // true

var array1 = [1, 2, 3, 4];
array1.fill(0, 2, 4);                     // array1 [1, 2, 0, 0]
[1, 2, 3].fill(4, 1, 1);                  // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2);                // [4, 2, 3]

function isBigEnough(element, index, array) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);  // [12, 130, 44]

var array1 = [5, 12, 8, 130, 44];
var found = array1.find(function(element, index, array) {
  return element > 10;
});                                        // 12

function isLargeNumber(element, index, array) {
  return element > 13;
}
array1.findIndex(isLargeNumber);           // 3

var arr1 = [1, 2, [3, 4]];
arr1.flat();                              // [1, 2, 3, 4]
var arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();                              // [1, 2, 3, 4, [5, 6]]
var arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);                             // [1, 2, 3, 4, 5, 6]
arr3.flat(Infinity);                      // [1, 2, 3, 4, 5, 6]

var arr1 = [1, 2, 3, 4];
arr1.map(x => [x * 2]);                  // [[2], [4], [6], [8]]
arr1.flatMap(x => [x * 2]);              // [2, 4, 6, 8]
arr1.flatMap(x => [[x * 2]]);            // [[2], [4], [6], [8]]

const items = ['item1', 'item2', 'item3'];
const copy = [];
items.forEach(function(item){
  copy.push(item);
});                                      // ["item1", "item2", "item3"]

[1, 2, 3].includes(2);                   // true
[1, 2, 3].includes(4);                   // false
[1, 2, 3].includes(3, 3);                // false

var array = [2, 5, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2

var a = ['Wind', 'Rain', 'Fire'];
var myVar1 = a.join();      // myVar1的值变为"Wind,Rain,Fire"
var myVar2 = a.join(', ');  // myVar2的值变为"Wind, Rain, Fire"

var arr = ["a", , "c"];
var sparseKeys = Object.keys(arr);    // ['0', '2']
var denseKeys = [...arr.keys()];      // [0, 1, 2]

var animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];
console.log(animals.lastIndexOf('Dodo'));          // 3

var array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);     // [2, 8, 18, 32]

let myFish = ["angel", "clown", "mandarin", "surgeon"];
let popped = myFish.pop();               // "surgeon"

var sports = ["soccer", "baseball"];
var total = sports.push("football", "swimming");   // 4

[0, 1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array){
  return accumulator + currentValue;
});                                                // 10

const array1 = [[0, 1], [2, 3], [4, 5]].reduceRight(
  (accumulator, currentValue) => accumulator.concat(currentValue)
);                                       // [4, 5, 2, 3, 0, 1]

var array1 = ['one', 'two', 'three'];
var reversed = array1.reverse();    //  Array ['three', 'two', 'one']

var array1 = [1, 2, 3];
var firstElement = array1.shift();   // 1

var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
var citrus = fruits.slice(1, 3);   // ["Orange", "Lemon"]

function isBiggerThan10(element, index, array) {
  return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);             // false
[12, 5, 8, 1, 4].some(isBiggerThan10);            // true

var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});                 // [1, 2, 3, 4, 5]

var myFish = ["angel", "clown", "mandarin", "sturgeon"];
var removed = myFish.splice(2, 0, "drum");   // []  
myFisha;     // ["angel", "clown", "drum", "mandarin", "sturgeon"]
removed = myFisha.splice(3, 1);  // ["mandarin"]
myFisha;     // ["angel", "clown", "drum", "sturgeon"]

var array1 = [1, 2, 'a', '1a'];
console.log(array1.toString());       // "1,2,a,1a"

var array1 = [1, 2, 3];
console.log(array1.unshift(4, 5));    // [4, 5, 1, 2, 3]

const array1 = ['a', 'b', 'c'];
const iterator = array1.values();  // 返回一个新的 Array Iterator 对象
for (const value of iterator) {
  console.log(value); // expected output: "a" "b" "c"
}
``` 
