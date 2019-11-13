## Location

1.Location 对象包含有关当前 URL 的信息，是 Window 对象的一个部分，可通过 window.location 属性来访问。
```
// "http://www.w3school.com.cn/jsref/dom_obj_location.asp"
window.location.href; 
window.location.hash; // "",设置或返回从井号 (#) 开始的 URL（锚）
window.location.host; // "www.w3school.com.cn"，包含端口号
window.location.hostname; // "www.w3school.com.cn"
window.location.port; // ""，默认端口80
window.location.pathname; // "/jsref/dom_obj_location.asp"
window.location.protocol; // "http:"
window.location.search; // ""，设置或返回从问号 (?) 开始的 URL（查询部分）

location.assign(URL) // window.location.assign("http://www.w3school.com.cn")
location.reload(force) // window.location.reload()，重新加载当前文档
location.replace(newURL) // ...location.replace("http://www.w3school.com.cn")
```

2.window.onhashchange：当 一个窗口的 hash （URL 中 # 后面的部分）改变时就会触发 hashchange 事件。
```
window.onhashchange = funcRef;
// 或者
<body onhashchange="funcRef();">
// 或者
window.addEventListener("hashchange", funcRef, false);
```

## pushState

1.window.history
```
window.history.back();  // 在history中向后跳转
window.history.forward();  // 向前跳转
window.history.go(-1);  // 等同于调用 back()
window.history.go(1);  // 等同于调用 forward()
window.history.length;  // 确定的历史堆栈中页面的数量
```

2.history.pushState(stateObj, "page 2", "bar.html");
- 状态对象 — 状态对象state是一个JavaScript对象，通过pushState () 创建新的历史记录条目。无论什么时候用户导航到新的状态，popstate事件就会被触发，且该事件的state属性包含该历史记录条目状态对象的副本。
- 标题 — Firefox 目前忽略这个参数，但未来可能会用到。在此处传一个空字符串应该可以安全的防范未来这个方法的更改。或者，你可以为跳转的state传递一个短标题。
- URL — 该参数定义了新的历史URL记录。注意，调用 pushState() 后浏览器并不会立即加载这个URL，但可能会在稍后某些情况下加载这个URL，比如在用户重新打开浏览器时。
- 注意 pushState() 绝对不会触发 hashchange 事件，即使新的URL与旧的URL仅哈希不同也是如此。
```
let stateObj = {
    foo: "bar",
};
// 这将使浏览器地址栏显示为 http://mozilla.org/bar.html，但并不会导致浏览器加载 bar.html ，甚至不会检查bar.html 是否存在
history.pushState(stateObj, "page 2", "bar.html");
```

3.history.pushState(stateObj, "page 2", "bar.html");
- replaceState() 的使用场景在于为了响应用户操作，你想要更新状态对象state或者当前历史记录的URL。
```
let stateObj = {
    foo: "bar",
};
history.pushState(stateObj, "page 2", "bar.html");

// 这将会导致地址栏显示http://mozilla.org/bar2.html,，但是浏览器并不会去加载bar2.html 甚至都不需要检查 bar2.html 是否存在
history.replaceState(stateObj, "page 3", "bar2.html");
```

4. let currentState = history.state;  获取当前状态

5. window.onpopstate：每当活动的历史记录项发生变化时， popstate 事件都会被传递给window对象。如果当前活动的历史记录项是被 pushState 创建的，或者是由 replaceState 改变的，那么 popstate 事件的状态属性 state 会包含一个当前历史记录状态对象的拷贝。
```
window.onpopstate = function(event) {
  alert("location: " + document.location + ", state: " + JSON.stringify(event.state));
};
//绑定事件处理函数. 
history.pushState({page: 1}, "title 1", "?page=1");    //添加并激活一个历史记录条目 http://example.com/example.html?page=1,条目索引为1
history.pushState({page: 2}, "title 2", "?page=2");    //添加并激活一个历史记录条目 http://example.com/example.html?page=2,条目索引为2
history.replaceState({page: 3}, "title 3", "?page=3"); //修改当前激活的历史记录条目 http://ex..?page=2 变为 http://ex..?page=3,条目索引为3
history.back(); // 弹出 "location: http://example.com/example.html?page=1, state: {"page":1}"
history.back(); // 弹出 "location: http://example.com/example.html, state: null
history.go(2);  // 弹出 "location: http://example.com/example.html?page=3, state: {"page":3}
```
