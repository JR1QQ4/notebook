## 面向对象

1.JavaScript 常被描述为一种基于原型的语言 (prototype-based language)——每个对象拥有一个原型对象，对象以其原型为模板、从原型继承方法和属性。

（1）prototype 属性：继承成员被定义的地方。类的prototype指向类的原型，缺省状态下，构造器的 prototype 属性初始为空白。类的prototype的__proto__指向继承的父类的prototype原型。
```
function Person(first, last, age, gender, interests) {
  this.name = {
    'first': first,
    'last': last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.bio = function() {
    alert(this.name.first + ' ' + this.name.last + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  };
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name.first + '.');
  };
};
Object.getPrototypeOf(Person.__proto__) === Object.prototype; // true
Person.prototype.__proto__ === Object.prototype; // true
```

（2）Object.create() 
```
var person1 = new Person('Bob', 'Smith', 32, 'male', ['music', 'skiing']);
var person2 = Object.create(person1);
person2.__proto__;  // 结果返回对象person1
```

（3）constructor 属性
```
person1.constructor;  // 返回 Person() 构造器
person2.constructor;  // 返回 Person() 构造器

var person3 = new person1.constructor('Karen', 'Stephenson', 26, 'female', ['playing drums', 'mountain climbing']);
person1.constructor.name;  // 获得某个对象实例的构造器的名字
```

（4）修改原型
```
function Person(first, last, age, gender, interests) {
  // 属性与方法定义
  Person.prototype.fullName = this.name.first + ' ' + this.name.last;
};
Person.prototype.fullName = this.name.first + ' ' + this.name.last; // 此时this指window，返回undefined undefined
var person1 = new Person('Tammi', 'Smith', 32, 'neutral', ['music', 'skiing', 'kickboxing']);

Person.prototype.farewell = function() {
  alert(this.name.first + ' has left the building. Bye for now!');
}
```

2.原型式的继承：继承的对象函数并不是通过复制而来，而是通过原型链继承。

（1）不能继承原型属性和方法
```
function Person(first, last, age, gender, interests) {
    this.name = { first, last };
    this.age = age;
    this.gender = gender;
    this.interests = interests;
};
Person.prototype.greeting = function() {
    alert('Hi! I\'m ' + this.name.first + '.');
};
function Teacher(first, last, age, gender, interests, subject) {
    // 第一个参数指定您调用的函数里所有“this”指向的对象。其他的变量指明所有目标函数运行时接受的参数。
    // 传给call()的this，意味着this指向Teacher()函数
    Person.call(this, first, last, age, gender, interests);
    this.subject = subject;
}
var teacher1 = new Teacher('Tammi', 'Smith', 32, 'neutral', ['music', 'skiing', 'kickboxing'], 'science');
```

（2）设置 Teacher() 的原型和构造器引用
- 任何您想要被继承的方法都应该定义在构造函数的prototype对象里，并且永远使用父类的prototype来创造子类的prototype，这样才不会打乱类继承结构。
```
// 创建一个和Person.prototype一样的新的原型属性值，然后将其作为Teacher.prototype的属性值
Teacher.prototype = Object.create(Person.prototype);

// 这导致自己的构造函数不指向自己，需要重新指定构造函数
Teacher.prototype.constructor === Person;  // true
Teacher.prototype.constructor = Teacher;
```

（3）在不同对象之间功能的共享通常被叫做 委托 - 特殊的对象将功能委托给通用的对象类型完成.

2.面向对象编程
- Namespace 命名空间： 在JavaScript中，命名空间只是另一个包含方法，属性，对象的对象。
- Class 类：定义对象的特征。它是对象的属性和方法的模板定义。
- Object 对象：类的一个实例。
- Property 属性：对象的特征，比如颜色。
- Method 方法：对象的能力，比如行走。
- Constructor 构造函数：对象初始化的瞬间，被调用的方法。通常它的名字与包含它的类一致。
- Inheritance 继承：一个类可以继承另一个类的特征。
- Encapsulation 封装：一种把数据和相关的方法绑定在一起使用的方法。
- Abstraction 抽象：结合复杂的继承，方法，属性的对象能够模拟现实的模型。
- Polymorphism 多态：多意为「许多」，态意为「形态」。不同类可以定义相同的方法或属性。

(1)命名空间
```
// 全局命名空间
var MYAPP = MYAPP || {};
// 子命名空间
MYAPP.event = {};
// 给普通方法和属性创建一个叫做MYAPP.commonMethod的容器
MYAPP.commonMethod = {
    regExForName: "", // 定义名字的正则验证
    regExForPhone: "", // 定义电话的正则验证
    validateName: function(name){
    // 对名字name做些操作，你可以通过使用“this.regExForname”
    // 访问regExForName变量
    },
    validatePhoneNo: function(phoneNo){
    // 对电话号码做操作
    }
}
// 对象和方法一起申明
MYAPP.event = {
    addListener: function(el, type, fn) {
    //  代码
    },
    removeListener: function(el, type, fn) {
    // 代码
    },
    getEvent: function(e) {
    // 代码
    }
    // 还可以添加其他的属性和方法
}
//使用addListener方法的写法:
MYAPP.event.addListener("yourel", "type", callback);
```

(2)标准内置对象：Math，Object，Array和String对象等
```
console.log(Math.random());
```

(2)自定义对象
```
function Person(firstName) {
  this.firstName = firstName;
}
Person.prototype.walk = function(){
  alert("I am walking!");
};
Person.prototype.sayHello = function(){
  alert("Hello, I'm " + this.firstName);
};
function Student(firstName, subject) {
  // 调用父类构造器, 确保(使用Function#call)"this" 在调用过程中设置正确
  Person.call(this, firstName);
  this.subject = subject;
};
// 建立一个由Person.prototype继承而来的Student.prototype对象.
// 注意: 常见的错误是使用 "new Person()"来建立Student.prototype.
// 这样做的错误之处有很多, 最重要的一点是我们在实例化时
// 不能赋予Person类任何的FirstName参数
// 调用Person的正确位置如下，我们从Student中来调用它
Student.prototype = Object.create(Person.prototype); // See note below
// 设置"constructor" 属性指向Student
Student.prototype.constructor = Student;
// 更换"sayHello" 方法
Student.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName + ". I'm studying " + this.subject + ".");
};
// 加入"sayGoodBye" 方法
Student.prototype.sayGoodBye = function(){
  console.log("Goodbye!");
};
// 测试实例:
var student1 = new Student("Janet", "Applied Physics");
student1.sayHello();   // "Hello, I'm Janet. I'm studying Applied Physics."
student1.walk();       // "I am walking!"
student1.sayGoodBye(); // "Goodbye!"
console.log(student1 instanceof Person);  // true 
console.log(student1 instanceof Student); // true

function createObject(proto) {
    function ctor() { }
    ctor.prototype = proto;
    return new ctor();
} // 使用一个function来获得相同的返回值，兼容Object.create
Student.prototype = createObject(Person.prototype);

// 封装：对于所有继承自父类的方法，只需要在子类中定义那些你想改变的即可。
// 抽象：JavaScript通过继承实现具体化，通过让类的实例是其他对象的属性值来实现组合。
// JavaScript Function 类继承自Object类（这是典型的具体化） 。Function.prototype的属性是一个Object实例（这是典型的组合）。
var foo = function(){};
console.log( 'foo is a Function: ' + (foo instanceof Function) ); // logs "foo is a Function: true"
console.log( 'foo.prototype is an Object: ' + (foo.prototype instanceof Object) ); // logs "foo.prototype is an Object: true"

// 多态：就像所有定义在原型属性内部的方法和属性一样，不同的类可以定义具有相同名称的方法;方法是作用于所在的类中。并且这仅在两个类不是父子关系时成立（继承链中，一个类不是继承自其他类）。
```

3.面向对象编程
```
// Object与Function关系
console.log(Function instanceof Object);  // true
console.log(Object instanceof Function);  // true

var f = new Function();
var o = new Object();
console.log(f instanceof Function);  //true
console.log(o instanceof Function);  // false
console.log(f instanceof Object);    // true
console.log(o instanceof Object);   // true

// Function.prototype是Object的实列 但是Object.prototype不是Function的实列
console.log(Function.prototype instanceof Object);  //true
console.log(Object.prototype instanceof Function);  // false

if(typeof Object.create !== 'function') {  // 复制继承
    Object.create = function(o) {
        var F = new Function();
        F.prototype = o;
        return new F();
    }
}
var a = {
    name: 'longen',
    getName: function(){
        return this.name;
    }
};
var b = {};
b = Object.create(a);
console.log(typeof b); //object
console.log(b.name);   // longen
console.log(b.getName()); // longen

var obj = {
    "name":'tugenhua',
    "age":'28'
};
for(var i in obj) {
    if(obj.hasOwnProperty(i)) {
        console.log(obj[i]); //tugenhua 28
    }
}


function A(x) {
    this.x = x;
    this.say = function(){    return this.x;}
}
function B(x,y) {
    this.m = A; // 把构造函数A作为一个普通函数引用给临时方法m
    this.m(x);  // 执行构造函数A;
    delete this.m; // 清除临时方法this.m
    this.y = y;
    this.method = function(){   return this.y;}
}
var a = new A(1);
var b = new B(2,3);
console.log(a.say()); //输出1, 执行构造函数A中的say方法
console.log(b.say()); //输出2, 能执行该方法说明被继承了A中的方法
console.log(b.method()); // 输出3， 构造函数也拥有自己的方法
```

（1）使用封装类实现继承
```
function extend(Sub,Sup) {    //Sub表示子类，Sup表示超类
    var F = function(){};    // 首先定义一个空函数
    F.prototype = Sup.prototype;   // 设置空函数的原型为超类的原型
    Sub.prototype = new F();  // 实例化空函数，并把超类原型引用传递给子类
    Sub.prototype.constructor = Sub;  // 重置子类原型的构造器为子类自身
    Sub.sup = Sup.prototype;     // 在子类中保存超类的原型,避免子类与超类耦合
    if(Sup.prototype.constructor === Object.prototype.constructor) {
        Sup.prototype.constructor = Sup;  // 检测超类原型的构造器是否为原型自身
    }
}
function A(x) { // 下面我们定义2个类A和类B，我们目的是实现B继承于A
    this.x = x;
    this.getX = function(){
        return this.x;
    }
}
A.prototype.add = function(){
    return this.x + this.x;
}
A.prototype.mul = function(){
    return this.x * this.x;
}
function B(x){  // 构造函数B
    A.call(this,x);   // 继承构造函数A中的所有属性及方法
}
extend(B,A);  // B继承于A
B.prototype.add = function(){
    //return this.x + "" + this.x;
    return B.sup.add.call(this);
}
console.log(b.add()); // 22
var b = new B(11);
console.log(b.getX()); // 11
console.log(b.add());  // 22
console.log(b.mul());  // 121
```
