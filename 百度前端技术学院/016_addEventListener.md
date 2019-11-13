## 事件

1.event
（1）属性
```
// 返回一个布尔值,表明当前事件是否会向DOM树上层元素冒泡.
var bool = event.bubbles; 

// 如果该事件的 cancelable 属性为 false, 则该事件的监听器无法阻止默认行为,调用preventDefault() 将产生错误.
var bool = event.cancelable; 

// Event.cancelBubble 属性是 Event.stopPropagation()的一个曾用名,设置为true可阻止事件的传播
event.cancelBubble = bool;
let bool = event.cancelBubble;

// 标识是当事件沿着 DOM 触发时事件的当前目标。它总是指向事件绑定的元素，而 Event.target 则是事件触发的元素。
var currentEventTarget = event.currentTarget;

// 返回一个布尔值，表明当前事件是否调用了 event.preventDefault()方法。
bool = event.defaultPrevented

// 表示事件流当前处于哪一个阶段。0-未被处理，1-事件正在被目标元素的祖先对象处理，2-事件对象已经抵达目标，3-事件对象逆向向上传播回目标元素的祖先元素
var phase = event.eventPhase;

// 触发事件的对象 (某个DOM元素) 的引用。当事件处理程序在事件的冒泡或捕获阶段被调用时，它与event.currentTarget不同。
let theTarget = event.target

// 只读属性 Event.type 会返回一个字符串, 表示该事件对象的事件类型。
event.type;
```

（2）方法
```
// 告诉user agent：如果此事件没有被显式处理，那么它默认的动作也不要做（因为默认是要做的）。此事件还是继续传播，除非碰到事件侦听器调用stopPropagation() 或stopImmediatePropagation()，才停止传播。
event.preventDefault();

// 阻止捕获和冒泡阶段中当前事件的进一步传播。
event.stopPropagation();
```

2.addEventListener
```
target.addEventListener(type, listener[, options]);
target.addEventListener(type, listener[, useCapture]);
```
（1）options
- capture:  Boolean，表示 listener 会在该类型的事件捕获阶段传播到该 EventTarget 时触发。
- once:  Boolean，表示 listener 在添加之后最多只调用一次。如果是 true， listener 会在其被调用之后自动移除。
- passive: Boolean，设置为true时，表示 listener 永远不会调用 preventDefault()。如果 listener 仍然调用了这个函数，客户端将会忽略它并抛出一个控制台警告。

（2）useCapture  
- 可选。布尔值，指定事件是否在捕获或冒泡阶段执行。
- true - 事件句柄在捕获阶段执行
- false- false- 默认。事件句柄在冒泡阶段执行
```
<div id="myDiv">
    <p id="myP">点击该段落， 我是冒泡</p>
</div><br>
<div id="myDiv2">
    <p id="myP2">点击该段落， 我是捕获</p>
</div>

// useCapture设置为false则先触发里面的alert，再触发父级元素的alert，即冒泡
document.getElementById("myP").addEventListener("click", function() 
{
    alert("你点击了 P 元素!");
}, false);
document.getElementById("myDiv").addEventListener("click", function()
{
    alert("你点击了 DIV 元素!");
}, false);
document.getElementById("myP2").addEventListener("click", function() 
{
    alert("你点击了 P 元素!");
}, true);
document.getElementById("myDiv2").addEventListener("click", function() 
{
    alert("你点击了 DIV 元素!");
}, true);
```

