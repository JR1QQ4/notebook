## 设计模式

1.工厂模式创建对象时无需指定创建对象的具体类。作用：多态，类与类之间的松耦合。通过工厂方法（或类）创建的对象在设计上都继承了相同的父对象这个思想，它们都是实现专门功能的特定子类。
```
function extend(subClass, superClass) {
    var F = function() {};
    F.prototype = superClass.prototype;
    subClass.prototype = new F();
    subClass.prototype.constructor = subClass;
    subClass.superclass = superClass.prototype;
    if(superClass.prototype.constructor == Object.prototype.constructor) {
        superClass.prototype.constructor = superClass;
    }
}

function SP(){this.cls = "super class";}   
SP.prototype.print = function(){alert(this.cls);};   
function SB(){}   
SB.prototype = new SP();   
new SB().print();  // super class
function F(){}   
F.prototype = SP.prototype;   
SB.prototype = new F();   
new SB().print();  // undefined
```

（1）案例
```
function CarMaker() {
    }
    CarMaker.prototype.drive = function () {
        console.log("I have " + this.doors + " doors.");
    };
    CarMaker.factory = function (type) {
        var constr = type, newcar;
        if (typeof CarMaker[constr] !== "function") {
            throw {
                name: "ERROR",
                message: constr + " doesn't exist."
            };
        }
        if (typeof CarMaker[constr].prototype.drive !== "function") {
            CarMaker[constr].prototype = new CarMaker();
        }
        newcar = new CarMaker[constr]();
        return newcar;
    };
    CarMaker.compact = function () {    this.doors = 4;};
    CarMaker.SUV = function () {    this.doors = 24;};
    var car1 = CarMaker.factory("compact");
```

2.命令模式：主要用途是把调用对象（用户界面，API和代理等）与实现操作的对象隔离开。分离任务的请求者与执行者（谁做和做什么的分离），分离了不变的抽象内容与多变的具体内容
-  [参考文档](https://www.jianshu.com/p/7fe95753ce0f)
```
// 这里抽象定义了请求者何时请求任务。
var setCommand = function(button, command) {
    button.onclick = function() {
        command.execute();
    }
}
// 这里抽象定义了任务执行者要做什么，
var SomeCommand = function(receiver) {
    this.receiver = receiver;
}
// execute，undo是约定俗成的
SomeCommand.prototype.execute = function(){
    this.receiver.doSomething;
}
SomeCommand.prototype.undo = function(){
    this.receiver.undoSomething;
}

// 这里选择具体的任务执行者
receiver = {doSomething: function(){}, undoSomething:function(){}};
var command = new SomeCommand(receiver)
// 这里选择任务请求者
setCommand(button, command)
// 也可以直接button.onclick = command.execute;
// 这里是规定了使用command.execute来实现解耦
// 因为setCommand不够抽象，所以以后还是会常变，怎么写都无所谓了，还是要改。
```

3.责任链模式：又称职责链模式，是一种对象的行为模式；它是一种链式结构，每个节点都有可能两种操作，要么处理该请求停止该请求操作，要么把请求转发到下一个节点，让下一个节点来处理请求；该模式定义了一些可能的处理请求的节点对象，请求的起点跟顺序都可能不一样，处理的节点根据请求的不一样而不同；请求者不必知道数据处理完成是由谁来操作的，内部是一个黑箱的操作过程，这是它的一个核心内容。、
-  抽象处理者角色：定义处理方法，以配置是否具有下个节点(Handler)对象;
-  具体处理者角色：定义处理方法的具体执行逻辑，判断是否可以处理该请求，如果可以就处理（返回结果结束）；如果不行，就查看是有下个节点，有的话就传递给下家；
```
function Handler() {
    this.next = null;
    this.setNext = function(_handler) {
        this.next = _handler;
    };
    this.handleRequest = function(money) {}
};
function CGBHandler = function() {}  //采购部
CGBHandler.prototype = new Handler();
CGBHandler.prototype.handleRequest = function(money) {
    if (money < 10000){  //处理权限最多10000
        console.log('同意');
    } else {
        console.log('金额太大，只能处理一万以内的采购');
        if (this.next) {
            this.next.handleRequest(money);
        }
    }
};
function ZJLHandler = function() {}  //总经理
ZJLHandler.prototype = new Handler();
ZJLHandler.prototype.handleRequest = function(money) {
    if (money < 100000){   //处理权限最多100000
        console.log('10万以内的同意');
    } else {
        console.log('金额太大，只能处理十万以内的采购');
        if (this.next) {
            this.next.handleRequest(money);
        }
    }
};
function DSZHandler = function() {}  //董事长
DSZHandler.prototype = new Handler();
DSZHandler.prototype.handleRequest = function(money) {
    if (money >= 100000){  //处理权限至少100000
        console.log('10万以上的我来处理');
    } 
};

function Client() {
    var cgb = new CGBHandler();
    var zjl = new ZJLHandler();
    var dsz = new DSZHandler();
    cgb.setNext(zjl);
    zjl.setNext(dsz);
    cgb.handleRequest(800000);
}
```

## Promise

1.Promise是抽象异步处理对象以及对其进行各种操作的组件。
```
var promise = new Promise(function(resolve, reject) {
    // 异步处理
    // 处理结束后、调用resolve 或 reject
});
promise.then(function(result){
    // 获取文件内容成功时的处理
}).catch(function(error){
    // 获取文件内容失败时的处理
});
```

（1）案例
```
function asyncFunction() {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            resolve('Async Hello world');
        }, 16);
    });
}
asyncFunction().then(function (value) {
    console.log(value);    // => 'Async Hello world'
}).catch(function (error) {
    console.log(error);
});
```

（2）promise对象有以下三个状态：
- Fulfilled：resolve(成功)时。此时会调用 onFulfilled
- Rejected：reject(失败)时。此时会调用 onRejected
- Pending：既不是resolve也不是reject的状态。也就是promise对象刚被创建后的初始化状态等

（3）案例
```
const getJSON = function(url) {
    const promise = new Promise(function(resolve, reject){
        const handler = function() {
            if (this.readyState !== 4) {
                return;
            }
            if (this.status === 200) {
                resolve(this.response);
            } else {
                reject(new Error(this.statusText));
            }
        };
        const client = new XMLHttpRequest();
        client.open("GET", url);
        client.onreadystatechange = handler;
        client.responseType = "json";
        client.setRequestHeader("Accept", "application/json");
        client.send();
    });
    return promise;
};
getJSON("/posts.json").then(function(json) {
    console.log('Contents: ' + json);
}, function(error) {
    console.error('出错了', error);
});
```

2.then...catch
```
aPromise
.then(function taskA(value){
    // task A
})
.then(function taskB(vaue){
    // task B
})
.catch(function onRejected(error){
    console.log(error);
});
```


[JavaScript设计模式--简单工厂模式](https://www.cnblogs.com/bfwbfw/p/7661020.html)
[javascript设计模式之工厂(Factory)模式](https://blog.csdn.net/vuturn/article/details/47955811)
[读书笔记之 - javascript 设计模式 - 命令模式](https://www.cnblogs.com/mrsai/p/3954072.html)
[[设计模式] javascript 之 责任链模式](https://www.cnblogs.com/editor/p/5679552.html)
[Promise](https://www.liaoxuefeng.com/wiki/1022910821149312/1023024413276544)
[JavaScript Promise迷你书](http://liubin.org/promises-book/)
