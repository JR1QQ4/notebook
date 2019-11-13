## Web API

### Web API 介绍
API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。
任何开发语言都有自己的API；API的特征输入和输出(I/O)；API的使用方法(console.log())

浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)，此处的Web API特指浏览器提供的API(一组方法)。

#### 常见的浏览器提供的API的调用方式
[mozilla](https://developer.mozilla.org/zh-CN/docs/Web/API)
JavaScript的组成：
* ECMAScript - JavaScript的核心 ：定义了javascript的语法规范，描述了语言的基本语法和数据类型
* BOM - 浏览器对象模型：一套操作浏览器功能的API，通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等
* DOM - 文档对象模型：一套操作页面元素的API，DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

## BOM

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

### BOM 对象 window
window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window。注意：window下一个特殊的属性 window.name

### 对话框
* alert()：显示一个警告对话框,上面显示有指定的文本内容以及一个"确定"按钮。
* prompt()：显示一个对话框，对话框中包含一条文字信息，用来提示用户输入文字。
* confirm()：显示一个具有一个可选消息和两个按钮(确定和取消)的模态对话框 。

## 页面加载事件
* ***onload*** ：在页面加载完的时候开始执行
```javascript
window.onload = function () {
// 当页面加载完成执行
// 当页面完全加载所有内容（包括图像、脚本文件、CSS 文件等）执行
}
```
* ***onunload***：关闭页面或 F5 时触发
```javascript
window.onunload = function () {
  // 当用户退出页面时执行
}  //  IE 可以使用 window.onbeforeunload 事件l
```

## 定时器
***setTimeout() 和 clearTimeout()***
在指定的毫秒数到达之后执行指定的函数，只执行一次
```javascript
var timerId = setTimeout(function () {
    console.log('Hello World');
}, 1000);  // 创建一个定时器，1000毫秒后执行，返回定时器的标示

clearTimeout(timerId);   // 取消定时器的执行

// 要想定时器循环执行，需要递归调用，自己调用自己，上面的方法修改如下
var timeId = ' ';
function fn(){
    console.log("Hello World");
	timeId = setTimeout(fn, 1000);
}
```
***setInterval() 和 clearInterval()***
定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数
```javascript
var timerId = setInterval(function () {
    var date = new Date();
	console.log(date.toLocaleTimeString());
}, 1000);  //  创建一个定时器，每隔1秒调用一次

clearInterval(timerId);  //  取消定时器的执行
```

## location 对象

location 对象是 window 对象的一个属性，调用的时候可以省略 window 对象
location 可以获取或者设置浏览器地址栏的 URL ( 统一资源定位符 Uniform Resource Locator )
```javascript
scheme://host:port/path?query#fragment
scheme: 通信协议，常用的 http,https,ftp,maito 等
port: 端口号，整数，可选，省略时使用方案的默认端口，http 默认端口为80
path: 路径，由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址
query: 查询，可选，用于给动态网页传递参数，可有多个参数，用'&'符号隔开，每个参数的名和值用'='符号隔开。例如：wd=菜鸟教程
fragment: 信息片断，字符串，锚点，如，#1

var url = document.createElement('a');
url.href = 'https://developer.mozilla.org/en-US/search?q=URL#search-results-close-container';
console.log(url.href);      // https://developer.mozilla.org/en-US/search?q=URL#search-results-close-container
console.log(url.protocol);  // https:
console.log(url.host);      // developer.mozilla.org
console.log(url.hostname);  // developer.mozilla.org
console.log(url.port);      // (blank - https assumes port 443)
console.log(url.pathname);  // /en-US/search
console.log(url.search);    // ?q=URL
console.log(url.hash);      // #search-results-close-container
console.log(url.origin);    // https://developer.mozilla.org
```
```javascript
//  Location没有继承任何方法，但实现了来自URLUtils的方法。

document.location.assign('https://developer.mozilla.org/zh-CN/docs/Web/API/Location.reload');  // 触发窗口加载并显示指定的 URL 的内容
window.location.reload(true);  // 重新加载当前页面  F5
document.location.replace('https://developer.mozilla.org/en-US/docs/Web/API/Location.reload');  // 以给定的URL来替换当前的资源，没有返回
```
```javascript
// 解析 URL 中的 query ，并返回对象的形式
function getQuery(queryStr) {
    var query = {};
    if (queryStr.indexOf('?') > -1) {
      var index = queryStr.indexOf('?');
      queryStr = queryStr.substr(index + 1);
      var array = queryStr.split('&');
      for (var i = 0; i < array.length; i++) {
        var tmpArr = array[i].split('=');
        if (tmpArr.length === 2) {
          query[tmpArr[0]] = tmpArr[1];
        }
      }
    }
    return query;
}
console.log(getQuery(location.search));
console.log(getQuery(location.href));
```

## history 对象
使用 history API与浏览器历史记录进行交互。***主要功能***：查找浏览器历史记录中出现过的页面，移除浏览器历史记录中的单个页面，向浏览器历史记录中添加页面，移除所有浏览器历史记录中的页面。
```javascript
window.history.forward();  //  前进，相当于浏览器左上角的 -->
window.history.back();   //  后退，相当于 <--
window.history.go(-1); // 相当于 <--
window.history.go(1); // 相当于 -->
```

## navigator 对象
Navigator 接口表示用户代理的状态和标识。 它允许脚本查询它和注册自己进行一些活动。可以使用只读的 window.navigator 属性检索导航器对象。
```javascript
window.navigator.appName;  // Netscape
window.navigator.appVersion; // 浏览器内核
window.navigator.language; // zh-CN
window.navigator.platform; // Win32 判断浏览器所在的系统平台类型.
window.navigator.userAgent; // 判断用户浏览器的类型，比appversion多一个Mozilla/
```
## DOM

文档对象模型（Document Object Model，简称DOM），是 [W3C](http://www.w3school.com.cn/) 组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为 DOM。

Document Object Model的历史可以追溯至1990年代后期微软与 [Netscape](http://baike.baidu.com/item/Netscape) 的“浏览器大战”，双方为了在 [JavaScript](http://baike.baidu.com/item/JavaScript) 与 [JScript](http://baike.baidu.com/item/JScript) 一决生死，于是大规模的赋予浏览器强大的功能。微软在网页技术上加入了不少专属事物，既有 [VBScript](http://baike.baidu.com/item/VBScript) 、 [ActiveX](http://baike.baidu.com/item/ActiveX) 、以及微软自家的 [DHTML](http://baike.baidu.com/item/DHTML) 格式等，使不少网页使用非微软平台及浏览器无法正常显示。DOM即是当时蕴酿出来的杰作。

DOM又称为文档树模型：

![DOM又称为文档树模型](./images/1497154623955.png)
* 文档：一个网页可以称为文档
* 节点：网页中的所有内容都是节点（标签、属性、文本、注释等）
* 元素：网页中的标签
* 属性：标签的属性

DOM经常进行的操作
* 查：获取元素
* 增：动态创建元素
* 删、改：对元素进行操作(设置其属性或调用其方法)
* 事件(什么时机做相应的操作)

### 获取页面元素

我们想要操作页面上的某部分(显示/隐藏，动画)，需要先获取到该部分对应的元素，才进行后续操作

#### 根据id获取元素
```javascript
var div = document.getElementById('main');  // id 为 main 的元素
console.log(div);
// 获取到的数据类型 HTMLDivElement，对象都是有类型的
// HTMLDivElement <-- HTMLElement <-- Element  <-- Node  <-- EventTarget
```
注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

#### 根据标签名获取元素
```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
    var div = divs[i];
	console.log(div);
}  //  获取到的 div 是一个对象数组，divs[0] 就是数组中第一个对象
```

#### 根据name获取元素
```javascript
var inputs = document.getElementsByName('hobby');
for (var i = 0; i < inputs.length; i++) {
    var input = inputs[i];
	console.log(input);
}    //   获取的也是一个对象数组，即使只有一个 hobby，但使用时需要有索引
```

#### 根据类名获取元素
```javascript
var mains = document.getElementsByClassName('main');
for (var i = 0; i < mains.length; i++) {
    var main = mains[i];
	console.log(main);
}  // 获取包含 main 类名的对象
```

#### 根据选择器获取元素
```javascript
var text = document.querySelector('#text');
console.log(text); // 获取 id 为 text 的元素，querySelecteer 中写法与css相同

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
    var box = boxes[i];
	 console.log(box);
}  // querySelectorAll 是获取所有
```

#### 总结
```javascript
一般使用：
    getElementById("id 属性的值")
	getElementsByTagName("标签 的名字")
以下的有些浏览器不支持，比如 IE 低版本：
    getElementsByName("name 属性的值")
	getElementsByClassName("类 样式的值")
	querySelector("选择器名字")
	querySelectorAll("选择器名字")
```

### 事件
事件：触发-响应机制
Event 接口表示在DOM中发生的任何事件，一些是用户生成的（例如鼠标或键盘事件），而其他由API生成。

***事件三要素***
* 事件源 ： 触发(被)事件的元素，哪个做 who
* 事件类型 ： 事件的触发方式(例如鼠标点击或键盘点击)，做什么 what
* 事件处理程序 ： 事件触发后要执行的代码(函数形式)，怎么做 do

#### 事件的基本使用
```javascript
<body><input type="button" value="点我" id="box" /></body>
<script>
var box = document.getElementById('box');
box.onclick = function() {
   console.log('代码会在box被点击后执行');  
} //  点击 box 按钮，控制台打印输出
</script>
```

### 属性操作

#### 非表单元素的属性
1. href、title、id、src、className
```javascript
var link = document.getElementById('link');
console.log(link.href);
console.log(link.title);

var pic = document.getElementById('pic');
console.log(pic.src);
```
2. innerHTML 和 innerText
```javascript
var box = document.getElementById('box');
box.innerHTML = '我是文本<p>我会生成为标签</p>';
console.log(box.innerHTML);
box.innerText = '我是文本<p>我不会生成为标签</p>';
console.log(box.innerText);
//  innnerHTML 会把内容中标签转为标签，innerText 不会
```
3. HTML转义符
```javascript
"		&quot;
‘		&apos;
&		&amp;
<		&lt;    //less than  小于
>		&gt;   // greater than  大于
空格	   &nbsp;
©		&copy;
```
4. innerText、textContent、innerHTML
```javascript
function setInerText(element,text){
    if((typeof element.textContent) == "undefined"){
        element.innerText = text;
    }else {
        element.textContent = text;
    }  //  目前浏览器都支持 innerText，应该是属于 IE 的标准
}  //  textContent 本身是火狐支持，ie8 不支持  
function getInnerText(element) {
    if((typeof element.textContent) == "undefined"){
        return element.innerText;
    }else {
        return element.textContent;
    }   
}
//（1）设置标签及内容推荐使用 innerHTML
//（2）获取标签中的文本，可以用 innerText ，也可以用 innerHTML
//（3）既要获取标签，又要获取文本，用 innerHTML
```

#### 表单元素属性
* value 用于大部分表单元素的内容获取( ***option*** 除外)
* type 可以获取 input 标签的类型(输入框或复选框等)
* disabled 禁用属性(按钮禁用了就是不能点击)
* checked 复选框选中属性(选中了就是 true)
* selected 下拉菜单选中属性(选中了就是 true)
```javascript
document.getElementsByName("input2")[0].disabled = true;
document.getElementsByName("input1")[0].readOnly = true;
```

#### 自定义属性操作
* getAttribute() 获取标签行内属性
* setAttribute() 设置标签行内属性
* removeAttribute() 移除标签行内属性
* 与 element.属性(```类.属性名```)的区别: 上述三个方法用于获取任意的行内属性
```javascript
for(var i=0;i<lis.length;i++){
    lis[i].setAttribute("index",i);
	var index = this.getAttribute("index");
}
```

#### 样式操作
使用style方式设置的样式显示在标签行内
```javascript
var box = document.getElementById('box');
box.style.width = '100px';
box.style.height = '100px';
box.style.backgroundColor = 'red';
//  注意：通过样式属性设置宽高、位置的属性类型是字符串，需要加上px
// img 的宽高、table 的边框 自带的属性不需要带px
```

#### 类名操作
修改标签的 className 属性相当于直接修改标签的类名
```javascript
var box = document.getElementById('box');
box.className = 'clearfix';  // 添加 css 样式
```

### 创建元素的三种方式
1. ***document.write()***
```javascript
document.getElementById("btn").onclick = function(){
     document.write('新设置的内容<p>标签也可以生成</p>');
}
// 页面加载完毕后，通过这个方法创建元素，存在把其他内容清除掉的情况
```
2. ***innerHTML***
```javascript
var box = document.getElementById('box');
box.innerHTML = '新内容<p>新标签</p>';
//  每次创建就需要重新赋值，消耗性能
```
3. ***document.createElement()***
```javascript
var div = document.createElement('div');
document.body.appendChild(div);  //  添加到 body 中
```

#### 性能问题
* innerHTML 方法由于会对字符串进行解析，需要避免在循环内多次使用。
* 可以借助字符串或数组的方式进行替换，再设置给 innerHTML
* 优化后与 document.createElement 性能相近

### 节点操作
节点：页面中所有的内容都是节点（标签，属性，文本：文字、空格、换行）
文档：document-----页面中的顶级对象
元素：页面中所有标签和里面的内容，标签----元素----对象（通过 DOM 的方式来获取这个标签，得到的这个对象，此时这个对象叫 DOM 对象）
节点的属性：为了获取更多的节点，得到节点中的标签（元素），识别节点中的标签元素
节点的类型：1标签节点，2属性节点，3文本节点
```javascript
var body = document.body;
var div = document.createElement('div');
body.appendChild(div);   // 创建一个 div

var div1 = body.children[1]; div1.innerHTML = "1";
body.insertBefore(div,div1);  // 在上面创建的 div 之前插入一个 div1

body.removeChild(div1);  //  移除创建的 div1

var text = document.createElement('p');
body.replaceChild(text, div);

var dvObj = document.getElementById("dv");
cosole.log(dvObj.parentNode);  //  获取 dv 的父节点
cosole.log(dvObj.parentNode.parentNode);  //  获取 dv 父节点的父节点

for(var i=0;i<dvObj.childNodes.length;i++){
     var node=dvObj.childNodes[i]; // 获取里面的每个子节点
   //nodeType--->节点的类型:1---标签,2---属性,3---文本
   //nodeName--->节点的名字:大写的标签--标签,小写的属性名---属性,#text---文本
   //nodeValue-->节点的值:标签---null,属性--属性的值,文本--文本内容
console.log(node.nodeType+"==="+node.nodeName+"==="+node.nodeValue);
}

console.log(dvObj.childNodes);  //  子节点
console.log(dvObj.children);  //  子元素
```

#### 节点层级
```javascript
<div id="dv">
<p>我是一个 p 标签</p>
    <ul id="u">
	<li>1</li>
	<li>2</li>
	<li id="th">3</li>
	<li>4</li>
	<li>5</li>
	<li>6</li>
	</ul>
</div>

var u = document.getElementById("u");
var th = document.getElementById("th");
console.log(u.parentNode);
console.log(u.parentElement);
console.log(u.childNodes); // 13  ，除了 li ，还包括空的换行的，子节点
console.log(u.children); // 6 ，6个 li ，子元素
console.log("======================================");
console.log(u.firstChild); // #text    第一个子节点，IE8 中是元素
console.log(u.firstElementChild);  // 1   IE8中不支持
console.log(u.lastChild); // #text    最后一个子节点，IE8 中是元素
console.log(u.lastElementChild); // 6    IE8中不支持 undefined
console.log(th.previousSibling); // #text   上一个兄弟节点
console.log(th.previousElementSibling);  // 2   元素
console.log(th.nextSibling); // #text    下一个兄弟节点
console.log(th.nextElementSibling);  // 4    元素

// 凡是获取节点的代码在谷歌和火狐得到的都是  相关的节点
// 凡是获取元素的代码在谷歌和火狐得到的都是   相关的元素
// 从子节点和兄弟节点开始,凡是获取节点的代码在IE8中得到的是元素,获取元素的相关代码,在IE8中得到的是undefined----元素的代码,iE中不支持
```
```javascript
//  获取第一个和最后一个元素兼容代码实现
function getFirstElementChild(ele) {
      if(ele.firstElementChild){
           return ele.firstElementChild;
      }else {
          var node = ele.firstChild;
          while(node && node.nodeType != 1){
              node = node.nextSibling;
          }
          return node;
      }
}
function getLastElementChild(ele){
      if(ele.lastElementChild){
          return ele.lastElementChild;
      }else {
          var node = ele.lastChild;
          while(node && node.nodeType != 1){
              node = node.previousSibling;
          }
          return node;
      }
}
```

#### 总结
* 节点操作，方法
	* appendChild()   增加节点
	* insertBefore()   插入节点
	* removeChild()   删除节点
	* replaceChild()    替换节点
* 节点层次，属性
	* parentNode   父节点
	* childNodes    子节点
	* children       子元素
	* nextSibling/previousSibling     下个/上个兄弟节点
	* firstChild/lastChild        第一个/最后一个节点

### 事件扩展

#### 注册/移除事件的三种方式
```javascript
//  注册：
// 1.对象.on时间名字 = 事件处理函数;    ==》同一个元素如果注册了多个事件，之前的事件会被覆盖
   document.getElementById("btn").onClick = function(){ };
// 2.对象.addEventListener("没有 on 的事件名字",事件处理函数,false);
   document.getElementById("btn").addEventListener("click",function(){},false);
// 3.对象.attachEvent("有 on 的事件名字",事件处理函数);
   document.attachEvent("onClick", function(){});

//  addEventListener  与  attachEvent 主要区别
// 1.参数个数不一样 addEventListener 三个参数，attachEvent 两个参数
// 2. addEventListener 谷歌,火狐,IE11支持,     IE8不支持
//     attachEvent 谷歌火狐不支持,IE11不支持,     IE8支持
// 3.this不同, addEventListener 中的 this 是当前绑定事件的对象
//     attachEvent 中的 this 是 window
// 4.addEventListener 中事件的类型(事件的名字)没有 on
//     attachEvent中的事件的类型(事件的名字)有 on

//  绑定事件兼容代码
function addEventListener(ele,type,fn){
    if(ele.addEventListener) {
	    ele.addEventListener(type,fn,false);
	} else if(ele.attachEvent) {
	    ele.attachEvent("on"+type,fn);
	} else {
	    ele["on"+type] = fn;
	}
}  //  ele 绑定事件元素，type 事件类型，fn 事件处理函数

// 移除绑定事件兼容代码
function removeEventListener(ele,type,fn){
    if(ele.removeEventListener) {
	    ele.removeEventListener(type, fn, false);
	} else if(ele.detachEvent) {
	    ele.detachEvent("on"+type, fn);
	} else {
	    ele["on"+type] = null;
	}
}
```

#### 事件三阶段
1. 事件捕获阶段 ： 事件从根节点流向目标节点，途中流经各个DOM节点，在各个节点上触发捕获事件，直到达到目标节点。从外向内
2. 事件目标阶段 ： 事件到达目标节点时，就到了目标阶段，事件在目标节点上被触发
3. 事件冒泡阶段 ： 事件在目标节点上触发后，不会终止，一层层向上冒，回溯到根节点。元素A中有元素B,都有相同的事件,里面的元素的事件触发了,外面元素的事件也会触发.可以是多个元素嵌套。从里向外
```javascript
//  阻止事件冒泡
window.event.cancelBubble=true;   //  谷歌,IE8支持,火狐不支持,window.event是一个对象,是IE中的标准
e.stopPropagation();   //   阻止事件冒泡---->谷歌和火狐支持,是火狐的标准

document.getElementById("dv2").onclick = function( ){
        console.log(arguments.length);  //  1
};  // 会发现默认会传入一个参数，是一个对象 MouseEvent，所以可以直接传入一个e

document.getElementById("btn").addEventListener("没有on的事件类型",事件处理函数,控制事件阶段的);
//  addEventListener中第三个参数是控制事件阶段的，
// 通过 e.eventPhase 可知道当前事件是什么阶段
// 如果这个属性的值是: 1---->捕获阶段，2---->目标阶段，3---->冒泡
```
***同一个元素绑定多个不同的事件***
```javascript
    function fn(e){
        switch(e.type) {
            case "click":
                console.log("点击事件");
                break;
            case "mouseover":
                console.log("鼠标进入事件");
                break;
            case "mouseout":
                console.log("鼠标移出事件");
                break;
            default:
                console.log("没有事件");
                break;
        }
    }
	document.getElementById("btn").onclick = fn;
    document.getElementById("btn").onmouseover = fn;
    document.getElementById("btn").onmouseout = fn;
```

#### 常用的鼠标和键盘事件
* onmouseup ：鼠标按键放开时触发
* onmousedown ：鼠标按键按下触发
* onmousemove  ：鼠标移动触发
* onkeyup ：键盘按键按下触发
* onkeydown ：键盘按键抬起触发
* onscroll ： 滚动条滑动触发

#### 事件对象的属性和方法
* event.clientX、event.clientY ：鼠标相对于浏览器窗口可视区域的X，Y坐标（窗口坐标），可视区域不包括工具栏和滚动条。IE事件和标准事件都定义了这2个属性，```谷歌中是 e.clientX，IE8中是 window.event.clientX```
* event.pageX、event.pageY ：类似于event.clientX、event.clientY，但它们使用的是文档坐标而非窗口坐标。这2个属性不是标准属性，但得到了广泛支持。IE事件中没有这2个属性。
* event.offsetX、event.offsetY ：鼠标相对于事件源元素（srcElement）的X,Y坐标，只有IE事件有这2个属性，标准事件没有对应的属性。
* event.screenX、event.screenY ：鼠标相对于用户显示器屏幕左上角的X,Y坐标。标准事件和IE事件都定义了这2个属性
* pageXOffset 和 pageYOffset 属性返回文档在窗口左上角水平和垂直方向滚动的像素。相等于 scrollX 和 scrollY 属性。
* event.target || event.srcElement 用于获取触发事件的元素，event.target.tagName 元素名字
* event.preventDefault() 取消默认行为，组织跳转
* $("a").click(function(event){  event.preventDefault();  });  //  不跳转
```javascript
//   鼠标移动，图片跟着动
document.onmousemove=function (e) {
   e = window.event || e;
    my$("im").style.left = window.event.clientX+"px";   // 可视区域的横坐标
    my$("im").style.top = window.event.clientY+"px";   // 可视区域的纵坐标
};
```

### 特效

#### 偏移量 offset
* offsetParent 用于获取定位的父级元素，有定位才能获取
* offsetParent 和 parentNode 的区别：parentNode 是获取节点
```javascript
//  offset 可以获取到 <style> 标签里的样式属性，返回不带 px 的数字
var box = document.getElementById('box');
console.log(box.offsetParent);
console.log(box.offsetLeft);  // 获取元素距离左边位置的值
console.log(box.offsetTop);  //  获取元素距离上面位置的值
console.log(box.offsetWidth);  // 获取元素的宽(有边框)
console.log(box.offsetHeight);  // 获取元素的高(有边框)

// 文档流中 ：
//  offsetLeft = 父级元素margin+父级元素padding+父级元素的border+自己的margin

// 脱离文档流 ：
//  主要是自己的 left 和自己的 margin
```

![offset](./images/1498743216279.png)

#### 滚动偏移 scroll
```javascript
var box = document.getElementById('box');
console.log(box.scrollLeft); //  向左卷曲出去的距离
console.log(box.scrollTop); //  向上卷曲出去的距离
console.log(box.scrollWidth);  // 元素中内容的实际的宽
console.log(box.scrollHeight);  // 元素中内容的实际的高
```

![scroll](./images/1498743288621.png)
```javascript
function getScroll() {
    return {   left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft || 0,
                   top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
        };
    }   //   获取页面向上或者向左卷曲出去的距离的值
	
	
function getAttrValue(element,attr) {
       return element.currentStyle ? element.currentStyle[attr] :    window.getComputedStyle(element,null)[attr]||0;
} //  获取元素的 <style> 标签中的任意属性值
```

#### 客户区大小 client
```javascript
var box = document.getElementById("box");
console.log(box.clientWidth); // 可视区域的宽(没有边框),边框内部的宽度
console.log(box.clientHeight); // 可视区域的高(没有边框),边框内部的高度
console.log(box.clientLeft); // 左边边框的宽度
console.log(box.clientTop);  // 上面的边框的宽度
```

![client](./images/1498743269100.png)

#### 总结
```
offset系列:偏移
(父级元素margin + 父级元素padding + 父级元素border + 自己的margin)
offsetLeft: 元素距离左边位置的值
offsetTop: 元素距离上面位置的值
offsetWidth: 获取元素的宽度(有边框)
offsetHeight: 获取元素的高度(有边框)

scroll系列:卷轴
scrollLeft: 元素向左卷曲出去的距离
scrollTop: 元素向上卷曲出去的距离
scrollWidth: 元素中内容的实际的宽度,如果没有内容,或者内容很少,元素的宽度
scrollHeight: 元素中内容的实际的高度,如果没有内容,或者内容很少,元素的高度

client系列:客户端
clientWidth: 可视区域的宽度,没有边框
clientHeight: 可视区域的高度,没有边框
clientLeft: 左边框的宽度
clientTop: 上边框的宽度
clientX: 可视区域的横坐标
clientY: 可视区域的纵坐标

//  鼠标移动的时候,文字不被选中
window.getSelection? window.getSelection().removeAllRanges():document.selection.empty();
```

---

# To Be Continue ...