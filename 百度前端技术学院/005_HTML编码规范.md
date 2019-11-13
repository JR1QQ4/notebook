## HTML 编码规范

### 代码风格

1、缩进与换行：
[强制] 使用 4 个空格做为一个缩进层级，不允许使用 2 个空格 或 tab 字符。
[建议] 每行不得超过 120 个字符。

2、命名：
[强制] class 必须单词全字母小写，单词间以 - 分隔。
[强制] class 必须代表相应模块或部件的内容或功能，不得以样式信息进行命名。
[强制] 元素 id 必须保证页面唯一。
[建议] id 建议单词全字母小写，单词间以 - 分隔。同项目必须保持风格一致。
[建议] id、class 命名，在避免冲突并描述清楚的前提下尽可能短。
[强制] 禁止为了 hook 脚本，创建无样式信息的 class。
[强制] 同一页面，应避免使用相同的 name 与 id。

3、标签
[强制] 标签名必须使用小写字母。
[强制] 对于无需自闭合的标签，不允许自闭合。
[强制] 对 HTML5 中规定允许省略的闭合标签，不允许省略闭合标签。
[强制] 标签使用必须符合标签嵌套规则。比如 div 不得置于 p 中，tbody 必须置于 table 中。
[建议] HTML 标签的使用应该遵循标签的语义。
```
p - 段落
h1,h2,h3,h4,h5,h6 - 层级标题
strong,em - 强调
ins - 插入
del - 删除
abbr - 缩写
code - 代码标识
cite - 引述来源作品的标题
q - 引用
blockquote - 一段或长篇引用
ul - 无序列表
ol - 有序列表
dl,dt,dd - 定义列表
```
[建议] 在 CSS 可以实现相同需求的情况下不得使用表格进行布局。
[建议] 标签的使用应尽量简洁，减少不必要的标签。

4、属性
[强制] 属性名必须使用小写字母。
[强制] 属性值必须用双引号包围。
[建议] 布尔类型的属性，建议不添加属性值。
[建议] 自定义属性建议以 xxx- 为前缀，推荐使用 data-。

### 通用

1、DOCTYPE
[强制] 使用 HTML5 的 doctype 来启用标准模式，建议使用大写的 DOCTYPE。
[建议] 启用 IE Edge 模式。<meta http-equiv="X-UA-Compatible" content="IE=Edge">
[建议] 在 html 标签上设置正确的 lang 属性。<html lang="zh-CN">

2、编码
[强制] 页面必须使用精简形式，明确指定字符编码。指定字符编码的 meta 必须是 head 的第一个直接子元素。
```
<html>
    <head>
        <meta charset="UTF-8">
        ......
    </head>
    <body>
        ......
    </body>
</html>
```
[建议] HTML 文件使用无 BOM 的 UTF-8 编码。

3、CSS 和 JavaScript 引入
[强制] 引入 CSS 时必须指明 rel="stylesheet"。
[建议] 引入 CSS 和 JavaScript 时无须指明 type 属性。
[建议] 展现定义放置于外部 CSS 中，行为定义放置于外部 JavaScript 中。
[建议] 在 head 中引入页面需要的所有 CSS 资源。
[建议] JavaScript 应当放在页面末尾，或采用异步加载。
```
<body>
    <!-- a lot of elements -->
    <script src="init-behavior.js"></script>
</body>
```
[建议] 移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 URL 协议部分与页面相同，建议省略协议前缀。
```
<script src="//s1.bdstatic.com/cache/static/jquery-1.10.2.min_f2fb5194.js"></script>
```

### head

1、title
[强制] 页面必须包含 title 标签声明标题。
[强制] title 必须作为 head 的直接子元素，并紧随 charset 声明之后。
```
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

2、favicon
[强制] 保证 favicon 可访问。
```
<link rel="shortcut icon" href="path/to/favicon.ico">
```

3、viewport
[建议] 若页面欲对移动设备友好，需指定页面的 viewport。

4、图片
[强制] 禁止 img 的 src 取值为空。延迟加载的图片也要增加默认的 src。
[建议] 避免为 img 添加不必要的 title 属性。
[建议] 为重要图片添加 alt 属性。
[建议] 添加 width 和 height 属性，以避免页面抖动。
[建议] 有下载需求的图片采用 img 标签实现，无下载需求的图片采用 CSS 背景图实现。

### 表单

1、控件标题
[强制] 有文本标题的控件必须使用 label 标签将其与其标题相关联。

2、按钮
[强制] 使用 button 元素时必须指明 type 属性值。
[建议] 尽量不要使用按钮类元素的 name 属性。

3、可访问性
[建议] 负责主要功能的按钮在 DOM 中的顺序应靠前。
[建议] 当使用 JavaScript 进行表单提交时，如果条件允许，应使原生提交功能正常工作。
```
当浏览器 JS 运行错误或关闭 JS 时，提交功能将无法工作。
如果正确指定了 form 元素的 action 属性和表单控件的 name 属性时，提交仍可继续进行
<form action="/login" method="post">
    <p><input name="username" type="text" placeholder="用户名"></p>
    <p><input name="password" type="password" placeholder="密码"></p>
</form>
```
[建议] 在针对移动设备开发的页面时，根据内容类型指定输入框的 type 属性。

### 多媒体

[建议] 当在现代浏览器中使用 audio 以及 video 标签来播放音频、视频时，应当注意格式。
[建议] 在支持 HTML5 的浏览器中优先使用 audio 和 video 标签来定义音视频元素。
[建议] 使用退化到插件的方式来对多浏览器进行支持。
```
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    <object width="100" height="50" data="audio.mp3">
        <embed width="100" height="50" src="audio.swf">
    </object>
</audio>

<video width="100" height="50" controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.ogg" type="video/ogg">
    <object width="100" height="50" data="video.mp4">
        <embed width="100" height="50" src="video.swf">
    </object>
</video>
```

[建议] 只在必要的时候开启音视频的自动播放。
[建议] 在 object 标签内部提供指示浏览器不支持该标签的说明。
```
<object width="100" height="50" data="something.swf">DO NOT SUPPORT THIS TAG</object>
```

### 模板中的 HTML

[建议] 模板代码的缩进优先保证 HTML 代码的缩进规则。
```
<!-- good -->
{if $display == true}
<div>
    <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
    </ul>
</div>
{/if}

<!-- bad -->
{if $display == true}
    <div>
        <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
        </ul>
    </div>
{/if}
```
[建议] 在循环处理模板数据构造表格时，若要求每行输出固定的个数，建议先将数据分组，之后再循环输出。

[参考地址](https://github.com/ecomfe/spec/blob/master/html-style-guide.md#%E5%BC%BA%E5%88%B6-%E9%A1%B5%E9%9D%A2%E5%BF%85%E9%A1%BB%E5%8C%85%E5%90%AB-title-%E6%A0%87%E7%AD%BE%E5%A3%B0%E6%98%8E%E6%A0%87%E9%A2%98)
