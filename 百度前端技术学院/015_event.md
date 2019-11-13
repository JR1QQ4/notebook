## Web安全之XSS攻防

1.XSS：跨站脚本攻击(Cross Site Scripting)，缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

2.原理：攻击者对含有漏洞的服务器发起XSS攻击（注入JS代码）；诱使受害者打开受到攻击的服务器URL；受害者在Web浏览器中打开URL，恶意脚本执行。

3.分类：
（1）反射型： 发出请求时，XSS代码出现在URL中，作为输入提交到服务器端，服务器端解析后响应，XSS随响应内容一起返回给浏览器，最后浏览器解析执行XSS代码，这个过程就像一次发射，所以叫反射型XSS。
（2）存储型: 存储型XSS和反射型的XSS差别就在于，存储型的XSS提交的代码会存储在服务器端（数据库，内存，文件系统等），下次请求目标页面时不用再提交XSS代码。

4.防御措施：
（1）编码：对用户输入的数据进行HTML Entity编码，"<" <=> "&lt;"
（2）过滤：移除用户上传的DOM属性，如onerror等，移除用户上传的style节点，script节点，iframe节点等
（3）校正：避免直接对HTML Entity编码，使用DOM Prase转换，校正不配对的DOM标签

## 事件

1.取消默认事件
```
if (event.defaultPrevented) {
    return; // 如果已取消默认操作，则不应执行任何操作
}

if (handled) {  // 定义的handled变量，判断事件是否触发
    event.preventDefault();// 如果事件已处理，则禁止“双重操作”
}
```
