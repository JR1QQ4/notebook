# HTML

>学习 HTML 需要理解 Web 语义化，以及标签的使用。

## Web 语义化

HTML最开始设计出来就是带有一定「语义」的，包括段落、表格、图片、标签等，但这些更多地只是方便浏览器 UA <sup>[1]</sup>对它们作合适的处理。但逐渐地，机器也要借助 HTML 提供的语义以及自然语言处理的手段来「读懂」它们从网上获取的 HTML 文档，但它们无法读懂例如「红色的文字」或者是深度嵌套的表格布局中内容的含义，因为太多已有的内容都是专门为了可视化的浏览器设计的。面对这种情况，出现了两种观点：

1. 我们可以让机器的理解能力越来越接近人类，人能看懂、听懂的东西，机器也能理解；
2. 我们应该在发布内容的时候，就用机器可读的、被广泛认可的语义信息来描述内容，来降低机器处理 Web 内容的难度

内容的语义表达能力和 AI 的智能程度决定了机器分析处理 Web 内容能力的高低。上面观点 1 的方向是朝着人类水平的人工智能努力，而观点 2 的方向正是万维网创始人 Tim Berners-Lee 爵士提出的美好愿景：语义网。语义网，简单来说就是让一切内容和包括对关系的描述都成为 Web 上的资源，都可以由唯一的 URI 定义，语义明确、机器可读。

HTML 规范其实一直在往语义化的方向上努力，许多元素、属性在设计的时候，就已经考虑了如何让各种用户代理甚至网络爬虫更好地理解 HTML 文档。HTML5 更是在之前规范的基础上，将所有表现层（presentational）的语义描述都进行了修改或者删除，增加了不少可以表达更丰富语义的元素。所谓语义本身就是对符号的一种共识，被认可的程度越高、范围越广，人们就越可以依赖它实现各种各样的功能。

HTML5 并非 Web 语义唯一倚仗的规范，除了 W3C 和 WHATWG 外，还有其它的组织在为扩展、标准化 Web 语义做着贡献。只要有浏览器厂商、搜索引擎原意支持，它们的规范一样可以成为通用的基础设施。例如 microformats 社区以及 [Schema](http://Schema.org) 上都有对 HTML 以及 [Microdata](http://www.w3.org/TR/html5/microdata.html) 规范的扩展词汇表，Google、Bing、Yahoo! 等搜索引擎以及各个主流浏览器都不同程度地接纳了其中定义的语义扩展，并应用在了生产中。

语义化作用：
1.方便代码的阅读和维护 2.同时让浏览器或是网络爬虫可以很好地解析，从而更好分析其中的内容 3.使用语义化标签会具有更好地搜索引擎优化

[1] 浏览器标识（UA）可以使得服务器能够识别客户使用的操作系统及版本、CPU 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件，从而判断用户是使用电脑浏览还是手机浏览，让网页作出自动的适应。

[参考，顾轶灵知乎回答](https://www.zhihu.com/question/20455165/answer/15176745)

## HTML 标签

1、HTML 元素
HTML 文档是由 HTML 元素定义的。HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

开始标签常被称为开放标签（opening tag），结束标签常称为闭合标签（closing tag）。标签通常是双标签，即有开放标签和闭合标签，单标签没有闭合标签或者说省略了闭合标签。没有内容的 HTML 元素被称为空元素。
```
<p>This is my first paragraph.</p>   --   <p> 元素
<br /> 或者 <br>   --   空元素
```

2、HTML 属性
属性为 HTML 元素提供附加信息。属性总是以名称/值对的形式出现，比如：name="value"。属性总是在 HTML 元素的开始标签中规定。
```
<a href="http://www.w3school.com.cn">This is a link</a>   --   href 属性
```


### 标题

HTML 标题（Heading）是通过 `<h1> - <h6>` 等标签进行定义的。
```
<h1>This is a heading</h1>   --   最大的标题，大标题
<h2>This is a heading</h2>
<h3>This is a heading</h3>
<h4>This is a heading</h4>
<h5>This is a heading</h5>
<h6>This is a heading</h6>   --   最小的标题
<hr />                       --   创建水平线
<!-- This is a comment -->   --   注释
<!--[if IE 8]>
    .... some HTML ....
<![endif]-->                 --   条件注释定义只有 IE 执行的 HTML 标签
```

### 段落

HTML 段落是通过 `<p>` 标签进行定义的。
```
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

### 链接

HTML 链接是通过 `<a>` 标签进行定义的。
```
<a href="http://www.w3school.com.cn">This is a link</a>
<a href="/example/html/lastpage.html">
<img border="0" src="/i/eg_buttonnext.gif" />
</a>
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>
<a href="http://www.w3school.com.cn/" target="_self">Visit W3School!</a>
<a href="http://www.w3school.com.cn/" target="_top">Visit W3School!</a>

<a href="#tips">跳转到固定章节</a>
```

### 图像

HTML 图像是通过 `<img>` 标签进行定义的。
```
<img src="http://www.w3school.com.cn/i/w3school_logo_white.gif" />
<img src="boat.gif" alt="Big Boat">
<img src ="/i/eg_cute.gif" align ="left"> 
<img src ="/i/eg_cute.gif" align ="right">
```

### 文本格式化

HTML 可定义很多供格式化输出的元素，比如粗体和斜体字。
```
<b></b> 或者 <strong></strong>   --   粗体
<i></i> 或者 <em></em>           --   斜体
<ins></ins>                      --   下划线
<del></del>                      --   删除线
<sup></sup> <sub><sub>           --   上标字和下标字 

<code></code>                    --   定义计算机代码
<pre></pre>                      --   定义预格式文本，原样输出
<var></var>                      --   定义变量

<q>构建人与自然和谐共存的世界。</q>                     --   短引用
<blockquote>
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>                                        --   长引用
<abbr title="World Health Organization">WHO</abbr>   --   缩写或首字母缩略语
<address>
Written by Donald Duck.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>                                           --   联系信息，以斜体显示
<cite>The Scream</cite> by Edward Munch.             --   定义著作的标题
```

### 表格

使用 HTML 创建表格。
```
<table border="1">
  <caption>Monthly savings</caption>        ---  定义表格标题
  <thead>                                   ---  定义表格的页眉
    <tr>                                    ---  定义表格的行
      <th>Month</th>                        ---  定义表格的表头
      <th>Savings</th>
    </tr>
  </thead>
  <tbody>                                   ---  定义表格的主体
    <tr>
      <td>January</td>                      ---  定义表格单元
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
  <tfoot>                                   ---  定义表格的页脚
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>
</table>
```

### 列表

HTML 支持有序、无序和定义列表。
```
<ul type="disc">        --- 无序列表，type="disc | circle | square"
<li>Coffee</li>
<li>Milk</li>
</ul>

<ol>                    --- 有序列表，type="A | a | I | i",默认数字
<li>Coffee</li>
<li>Milk</li>
</ol>

<dl>                    --- 定义列表
<dt>Coffee</dt>            ---  定义项目
<dd>Black hot drink</dd>   ---  项目的描述
<dt>Milk</dt>
<dd>White cold drink</dd>
</dl>
```

### 块

HTML 元素分为块级元素、行内元素、行内块元素。
* 块级元素：独占一行，h1、p、div、ul、ol、li、table
* 行内元素：宽高无效，a、strong、b、em、i、del、s、ins、u、span
* 行内块元素：能设置宽高，img、input、td

### 类

对 HTML 进行分类（设置类），使我们能够为元素的类定义 CSS 样式。
```
<!DOCTYPE html>
<html>
<head>
<style>                    -- 内部样式表
  span.red {color:red;}    -- 元素和类选择器
</style>
</head>
<body>
<h1>My <span class="red">Important</span> Heading</h1> -- 类名red
</body>
</html>
```


### 布局

网站常常以多列显示内容（就像杂志和报纸）。
```
<body>                          ---  HTML
<div id="header">               ---  ID，和类名一样用于区分普通元素
<h1>City Gallery</h1>
</div>
<div id="nav">
London<br>
Paris<br>
Tokyo<br>
</div>
<div id="section">
<h1>London</h1>
<p>
London is the capital city of England. It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.
</p>
<p>
Standing on the River Thames, London has been a major settlement for two millennia,
its history going back to its founding by the Romans, who named it Londinium.
</p>
</div>
<div id="footer">
Copyright W3School.com.cn
</div>
</body>

<style>                           ---  内部样式表
#header {                         ---  ID 选择器
    background-color:black;
    color:white;
    text-align:center;
    padding:5px;
}
#nav {
    line-height:30px;
    background-color:#eeeeee;
    height:300px;
    width:100px;
    float:left;
    padding:5px; 
}
#section {
    width:350px;
    float:left;
    padding:10px; 
}
#footer {
    background-color:black;
    color:white;
    clear:both;
    text-align:center;
    padding:5px; 
}
</style>
```

HTML5 网站布局提供了新语义标签：
```
header   -- 文档或节的页眉
nav      -- 导航链接的容器
section  -- 独立的自包含文章
aside    -- 内容之外的内容（比如侧栏）
footer   -- 文档或节的页脚
details  -- 额外的细节
summary  -- details 元素的标题
```

### 响应式 Web 设计

响应式 Web 设计（Responsive Web Design），能够以可变尺寸传递网页。后面再深入学习。

### 框架

通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。
框架结构标签（&lt;frameset&gt;）：
* 框架结构标签（&lt;frameset&gt;）定义如何将窗口分割为框架
* 每个 frameset 定义了一系列行或列
* rows/columns 的值规定了每行或每列占据屏幕的面积
```
<html>
<frameset rows="50%,50%">                      --  两行
  <frame src="/example/html/frame_a.html" noresize="noresize">  -- 不支持拖拽
  <frameset cols="25%,75%">                    --  两列
    <frame src="/example/html/frame_b.html">
    <frame src="/example/html/frame_c.html">
  </frameset>
</frameset>
</html>
```

### Iframe

iframe 用于在网页内显示网页。
```
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
<iframe src="demo_iframe.htm" frameborder="0"></iframe> -- 删除边框

<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="http://www.w3school.com.cn" target="iframe_a">W3School.com.cn</a></p>  -- 使用 iframe 作为链接的目标
```

### 头部

&lt;head&gt; 元素是所有头部元素的容器。&lt;head&gt;内的元素可包含脚本，指示浏览器在何处可以找到样式表，提供元信息，等等。
以下标签都可以添加到 head 部分：&lt;title&gt;、&lt;base&gt;、&lt;link&gt;、&lt;meta&gt;、&lt;script&gt; 以及 &lt;style&gt;。

```
<head>
<title>Title of the document</title>
<meta name="description" content="Free Web tutorials on HTML, CSS, XML" />
<meta name="keywords" content="HTML, CSS, XML" />
<meta name="author" content="root,root@xxxx.com" /> 
<meta charset="UTF-8">
<meta http-equiv="charset" content="iso-8859-1">
<meta http-equiv="expires" content="31 Dec 2008">
<!-- 
content-type: text/html
charset:iso-8859-1
expires:31 Dec 2008
-->
<link rel="stylesheet" type="text/css" href="mystyle.css" />
<base href="http://www.w3school.com.cn/" />
<base target="_blank" />
<style type="text/css">
body {background-color:yellow}
</style>
<script type="text/javascript">
document.write("Hello World!")
</script>
</head>
```

#### title

title 定义浏览器工具栏中的标题，提供页面被添加到收藏夹时显示的标题，显示在搜索引擎结果中的页面标题。

#### base

base 标签为页面上的所有链接规定默认地址或默认目标（target）。

#### link

link 标签定义文档与外部资源之间的关系，最常用于连接样式表。

#### style

style 标签用于为 HTML 文档定义样式信息。

#### meta

meta 标签提供关于 HTML 文档的元数据，元数据（metadata）是关于数据的信息，元数据不会显示在页面上，但是对于机器是可读的。典型的情况是，meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。

#### script

script 标签用于定义客户端脚本，比如 JavaScript。

### 实体

HTML 中的预留字符必须被替换为字符实体。
小于号 - &lt; 或者 &#60;、大于号 - &gt; 或者 &#62;、版权 - &copy; 或者 &#169;、注册商标 - &reg; 或者 &#174;、元 - &yen; 或者 &#165;、商标 - &trade; 或者 &#8482;等等。  

### URL

URL 也被称为网址，遵守以下的语法规则：`scheme://host.domain:port/path/filename`
* scheme - 定义因特网服务的类型。最常见的类型是 http
* host - 定义域主机（http 的默认主机是 www）
* domain - 定义因特网域名，比如 w3school.com.cn
* :port - 定义主机上的端口号（http 的默认端口号是 80）
* path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
* filename - 定义文档/资源的名称
URL 编码会将字符转换为可通过因特网传输的格式。

### 文档类型

&lt;!DOCTYPE&gt; 声明帮助浏览器正确地显示网页,不是 HTML 标签,它为浏览器提供一项信息（声明），即 HTML 是用什么版本编写的。
```
<!DOCTYPE html>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

### 表单

HTML 表单用于搜集不同类型的用户输入。
```
<form action="action_page.php" method="post">
         User name:<br><input type="text" name="username"><br>
         User password:<br><input type="password" name="psw"><br>
        <input type="radio" name="gender" value="famale">female<br>
        <input type="radio" name="gender" value="male">male<br>
        <input type="checkbox" name="vehicle" value="Bike">I have a bike<br>
        <input type="checkbox" name="vehicle" value="Car">I have a car<br> 
        <input type="submit" value="submit"><br>
        <fieldset>
            <legend>Personal information:</legend>
            First name:<br>
            <input type="text" name="firstname" value="Mickey">
            <br>
            Last name:<br>
            <input type="text" name="lastname" value="Mouse">
            <br><br>
            <input type="submit" value="Submit">
        </fieldset>
        <select name="cars">
            <option value="volvo">Volvo</option>
            <option value="saab">Saab</option>
            <option value="fiat" selected>Fiat</option>
            <option value="audi">Audi</option>
        </select><br>
        <textarea name="message" rows="10" cols="30">
        The cat was playing in the garden.
        </textarea><br>
        <button type="button" onclick="alert('Hello World!')">Click Me!</button><br>
        Quantity:<input type="number" name="points" min="0" max="100" step="10" value="30"><br>
        Enter a date before 1980-01-01:
        <input type="date" name="bday" max="1979-12-31"><br>
        Enter a date after 2000-01-01:
        <input type="date" name="bday" min="2000-01-02"><br>
        Select your favorite color:<input type="color" name="favcolor"><br>
        <input type="range" name="points" min="0" max="10"><br>
        Birthday (month and year):<input type="month" name="bdaymonth"><br>
        Select a week:<input type="week" name="week_year"><br>
        Select a time:<input type="time" name="usr_time"><br>
        E-mail:<input type="email" name="email"><br>
        Search Google:<input type="search" name="googlesearch"><br>
        Telephone:<input type="tel" name="usrtel">
    </form>
```

#### Input 属性

value 属性规定输入字段的初始值
placeholder 属性规定用以描述输入字段预期值的提示（样本值或有关格式的简短描述）
required 属性是布尔属性，规定在提交表单之前必须填写输入字段
readonly 属性规定输入字段为只读（不能修改）
disabled 属性规定输入字段是禁用的，被禁用的元素是不可用和不可点击的，不会被提交
size 属性规定输入字段的尺寸（以字符计）
maxlength 属性规定输入字段允许的最大长度
autocomplete 属性规定表单或输入字段是否应该自动完成，值是 on、off
novalidate 属性属于 form 元素属性，在提交表单时不对表单数据进行验证
autofocus 属性是布尔属性，当页面加载时 input 元素应该自动获得焦点
form 属性规定 input 元素所属的一个或多个表单
formaction 属性规定当提交表单时处理该输入控件的文件的 URL
list 属性引用的 datalist 元素中包含了 input 元素的预定义选项
min 和 max 属性规定 input 元素的最小值和最大值
multiple 属性是布尔属性，

### HTML5 

HTML5 的一些最有趣的新特性：
* 新的语义元素，比如 &lt;header&gt;, &lt;footer&gt;, &lt;article&gt;, and &lt;section&gt;。
* 新的表单控件，比如数字、日期、时间、日历和滑块。
* 强大的图像支持（借由 &lt;canvas&gt; 和 &lt;svg&gt;）
* 强大的多媒体支持（借由 &lt;video&gt; 和 &lt;audio&gt;）
* 强大的新 API，比如用本地存储取代 cookie。

IE8 以及更早的版本，不允许对未知元素添加样式，Sjoerd Visscher 创造了 "HTML5 Enabling JavaScript", "the shiv"：
```
<!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
```
