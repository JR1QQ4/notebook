# JavaScript

1.选择器

```
getElementById("id属性的值")  ---> 返回一个对象
getElementsByTagName("标签名字")
getElementsByName("name属性的值")
getElementsByClassName("类样式的名字")  ---> 存在兼容问题，IE9+

querySelector(有效的CSS选择器字符串)
querySelectorAll(CSS selector)   --->  IE8+
```

2.事件

```
function my$(ele){
    return document.getElementById(ele);
}
my$("txt").onfocus=function(){}
my$("txt").onblur=function(){}
```

3.文本

```
textContent  // FF1+
innerText  // IE10+
innerHTML

function setInnerText(ele,text){
    if(typeOf ele.textContent == "undefined"){  // 不支持
        ele.innerText = text;
    }else {
        ele.textContent = text;
    }
}
function getInnerText(ele){
    if(typeOf ele.textContent == "undefined"){  // 不支持
        return ele.innerText;
    }else {
        return ele.textContent;
    }
}
```

4.自定义属性

```
setAttribute("key","value")
getAttribute("key")
removeAttribute("key")

className = ""  // 移除之后还有 class
removeAttribute("class")  // 移除之后没有 class
```

5.节点和元素

```
元素element  --- 标签 --- 对象
节点node  --- 标签，属性，文本（文字，换行，空格，回车）

nodeType：节点的类型，1---标签，2---属性，3---文本
nodeName：节点的名称，标签节点---大写的标签名字，属性节点---小写的属性名字，文本节点---#text
nodeValue：节点的值，标签节点---null，属性节点---属性值，文本节点---文本内容

ele.getAttributeNode("id")  --- 获取属性节点，返回一个节点

parentNode  --- 父级节点
childNodex  --- 子级节点，包含文本节点、属性节点
children  --- 子元素
```

6.12个获取节点和元素

```
<ul id="uu"><li>1</li><li id="se">2</li><li>3</li></ul>
var ul = document.getElementById("uu");
var li = document.getElementById("se");
ul.parentNode
ul.parentElement
ul.childNodes
ul.children
-------------------------------------
ul.firstChild
ul.firstElementChild
ul.lastChild
ul.lastElementChild
li.previousSibling
li.previousElementSibling
li.nextSibling
li.nextElementSibling

// 获取节点的代码在谷歌和火狐得到的都是 相关的节点
// 获取元素的代码在谷歌和火狐得到的是 相关的元素
// 获取子节点和兄弟节点，获取节点的代码在IE8中得到的是元素，获取元素的代码得到的是undefined
```

7.兼容代码

```
function getFirstElementChild(ele) {  // 获取第一个子元素，ele是父级元素
    if (ele.firstElementChild) {
        return ele.firstElementChild;
    } else {
        var node = ele.firstChild;
        while(node&&node.nodeType!==1){
            node=node.nextSibling;
        }
        return node;
    }
}
function getLastElementChild(ele) {  // 获取最后一个子元素
    if (ele.lastElementChild) {
        return ele.lastElementChild;
    } else {
        var node = ele.lastChild;
        while(node&&node.nodeType!==1){
            node=node.previousSibling;
        }
        return node;
    }
}
```

8.事件

```
    function addEventListener(ele, type, fn) {  // 绑定
        if (ele.addEventListener) {
            ele.addEventListener(type, fn, false);  // false表示冒泡阶段
        } else if (ele.attachEvent) {
            ele.attachEvent("on" + type, fn);
        } else {
            ele["on" + type] = fn;
        }
    }
    function removeEventListener(ele, type, fn) {  // 解绑
        if (ele.removeEventListener) {
            ele.removeEventListener(type, fn, false);  // true表示捕获阶段
        } else if (ele.detachEvent) {
            ele.detachEvent("on" + type, fn);
        } else {
            ele["on" + type] = null;
        }
    }
```

9.事件冒泡和阻止浏览器默认事件

```
    function stopPropagation(e) {
        e.stopPropagation ? e.stopPropagation():(window.event.cancelBubble=true);
    }
window.event.cancelBubble = true; // 谷歌，IE8支持，火狐不支持
e.stopPropagation();  // 谷歌和火狐支持

window.event.preventDefault();  // 存在兼容问题
return false;
```

10.offset、scroll、client

```
没有脱离文档流，offsetLeft = 父级元素的(margin + padding + border) + 自己的margin
脱离文档流，offsetLeft = 自己的(left + margin)
元素的宽高，有边框，有内边距无外边距 offsetWidth offsetHeight

scrollWidth scrollHeight：元素中内容的实际的宽高，没有边框；没有内容就是元素的宽高
scrollTop scrollLeft：卷曲的上边和左边

clientWidth clientHeight：可视区域的宽高，没有边框，边框内部的宽高
clientLeft clientTop：左上边框的边框宽度（内容到边框边缘）
clientX clientY：可是区域的横纵坐标
```

11.兼容pageX pageY clientX clientY

```
    function getScroll() {
        return {
            left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft,
            top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop
        }
    }
    var eventObj = {
        getEvent: function (evt) {
            return evt || window.event;
        },
        getClientX: function (evt) {
            return this.getEvent(evt).clientX;
        },
        getClientY: function (evt) {
            return this.getEvent(evt).clientY;
        },
        getScrollLeft: function () {
            return window.pageXOffset || document.body.scrollLeft || document.documentElement.scrollLeft || 0;
        },
        getScrollTop: function () {
            return window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop || 0;
        },
        getPageX: function (evt) {
            return this.getEvent(evt).pageX ? this.getEvent(evt).pageX : (this.getClientX(evt) + this.getScrollLeft());
        },
        getPageY: function (evt) {
            return this.getEvent(evt).pageY ? this.getEvent(evt).pageY : (this.getClientY(evt) + this.getScrollTop());
        }
    };
```

12.动画

```
    function animate(ele,target) {
        clearInterval(ele.timerId);
        ele.timerId = setInterval(function () {
            var current = ele.offsetLeft;
            var step = (target - current)/10;
            step = step>0?Math.ceil(step):Math.floor(step);
            current+=step;
            ele.style.left = current+"px";
            if(current==target){
                clearInterval(ele.timerId);
            }
            console.log("目标位置："+target+"，当前位置："+current+"，每次移动步数："+step);
        },20);
    }

    function getStyle(ele,attr) {  // 获取元素任意一个样式属性的值
        return window.getComputedStyle?window.getComputedStyle(ele,null)[attr]:ele.currentStyle[attr]||0;
    }
    function animate(ele,attr,target) {
        clearInterval(ele.timerId);
        ele.timerId = setInterval(function () {
            var current = parseInt(getStyle(ele,attr));
            var step = (target - current)/10;
            step = step>0?Math.ceil(step):Math.floor(step);
            current+=step;
            ele.style[attr] = current+"px";
            if(current==target){
                clearInterval(ele.timerId);
            }
            console.log("目标位置："+target+"，当前位置："+current+"，每次移动步数："+step);
        },20);
    }

    function animatePro(ele,json,fn) {
        clearInterval(ele.timerId);
        ele.timerId = setInterval(function () {
            var flag = true;
            for(var attr in json){
                if(attr=="opacity"){
                    var current = getStyle(ele,attr)*100;
                    var target = json[attr]*100;
                    var step = (target - current)/10;
                    step = step>0?Math.ceil(step):Math.floor(step);
                    current+=step;
                    ele.style[attr] = current/100;
                }else if(attr == "zIndex"){
                    ele.style[attr] = json[attr];
                }else {
                    var current = parseInt(getStyle(ele,attr));
                    var target = json[attr];
                    var step = (target - current)/10;
                    step = step>0?Math.ceil(step):Math.floor(step);
                    current+=step;
                    ele.style[attr] = current + "px";
                }
                if(current!=target){
                    flag = false;
                }
            }
            if(flag){
                clearInterval(ele.timerId);
                if(fn){
                    fn();
                }
            }
            console.log("目标位置："+target+"，当前位置："+current+"，每次移动步数："+step);
        },20);
    }
```

13.鼠标移动的时候，文字不被选中

```
window.getSelection()?window.getSelection().removeAllRanges():document.selection.empty();
```
