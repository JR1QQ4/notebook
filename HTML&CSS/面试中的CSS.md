# 面试中的CSS

层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。

## 盒模型

盒模型由 `margin + border + padding + content` 四个属性组成，分为两种：W3C的标准盒模型和IE盒模型。

W3C的标准盒模型：`width = content`，不包含 `border + padding`

IE盒模型：`width = border + padding + content`

相互转换：`box-sizing: content-box` 是W3C盒模型，`box-sizing: border-box` 是IE盒模型

## 垂直居中

```html
<div class="outer">
    <div class="inner"></div>
</div>
```

方法一：flex，`justify-content: center;align-items: center`

方法二：position + transform, 宽高未知

方法三：position + margin（负），宽高已知

方法四：子盒子`position: absolute;top: 0; right: 0;bottom: 0;left: 0;margin:auto`

[参考示例](http://dongqunren.gitee.io/notebook/interview/css/center.html)

## 三栏布局

```html
<div class="container">
    <div class="left">left</div>   
    <div class="right">right</div>
	 <div class="main">main</div>
</div>
```

方法一：flex，main放中间直接设置`flex:1`，放最后需要设置`order`

方法二：父盒子相对定位，左右绝对定位，main设置`main: 0 200px`

方法三：左盒子左浮动，右盒子有浮动，main设置`main: 0 200px`

[参考示例](http://dongqunren.gitee.io/notebook/interview/css/layout.html)

[其他布局](http://dongqunren.gitee.io/ife/projects/ife01/src/5/orther.html)

## 权重

CSS基本选择器包含ID选择器、类选择器、标签选择器、通配符选择器。 正常情况下，`!important > 行内样式 > ID选择器 > 类选择器 > 标签选择器 > 通配符选择器`。

权重取值：

- 内联样式，权值为1000
- ID选择器，权值为0100
- 类，伪类和属性选择器，权值为0010
- 标签选择器和伪元素选择器，权值为0001
- 通配符、子选择器、相邻选择器等，权值为0000
- 继承的样式没有权值

如果权重相同时，CSS遵循就近原则。也就是说靠近元素的样式具有最大的优先级，或者说排在最后的样式优先级最大。

如果层级相同，继续往后比较，如果层级不同，层级高的权重大，不论低层级有多少个选择器。

## BFC

BFC（Block Formatting Context）块格式化上下文。BFC元素特性，内部子元素不会影响到外部元素。

什么时候会触发BFC：

- 根元素(html)
- `float`的值不为`none`
- `overflow`的值为`auto`,`scroll`或`hidden`
- `position`的值不为`relative`和`static`
- `display`的值为`table-cell(表格单元格)`, `table-caption(表格标题)`, `inline-block(行内块元素)`中的任何一个
- 匿名表格单元格元素（元素的 display为 table、table-row、table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）
- display 值为 flow-root 的元素
- contain 值为 layout、content或 paint 的元素
- 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
- 网格元素（display为 grid 或 inline-grid 元素的直接子元素）
- 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）

BFC布局规则:

- 内部的box会在垂直方向，一个接一个的放置
- box垂直方向的距离有margin决定。属于同一个BFC的两个相邻box的margin会发生重叠。每个元素的左外边距与包含块的左边界相接触，即使浮动元素也是如此。
- BFC的区域不会与float的元素区域重叠
- 计算BFC的高度时，浮动子元素也参与计算
- BFC就是页面上一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然

BFC能解决的问题:

- 父元素塌陷
- 外边距重叠
- 清除浮动

BFC与自适应布局：

- `overflow:auto/hidden`  IE7+
- `display:inline-block` IE6/IE7
- `display:table-cell` IE8+

参考文章：[CSS深入理解流体特性和BFC特性下多栏自适应布局](https://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/)

## 清除浮动的方法

清除浮动主要是为了防止父元素塌陷，常用的是给父元素添加 `clearfix` 类，然后设置`.clearfix::before`和`.clearfix::after`。

方法一： clearfix，类似传统的添加一个额外标签，设置`clear:both;`

```css
.clearfix::after{
  content: "";
  display: block;
  height: 0;
  clear:both;
  visibility: hidden;
}

// 或者
.clearfix {
  // 由于IE6-7不支持:after，使用 zoom:1 触发 hasLayout
  *zoom: 1;
}
.clearfix:after {
  content: ""; 
  display: table; 
  clear: both;
}
```

方法二：触发父盒子BFC，`overflow:hidden|auto|scroll`

方法三：使用`before`和`after`双伪元素清除浮动

```css
.clearfix::before, .clearfix::after { 
  content:"";
  display:table;
}
.clearfix::after {
  clear:both;
}
.clearfix {
  *zoom:1;
}
```

## Flex布局和Grid布局

[Grid布局和Flex布局](https://www.cnblogs.com/dongqunren/p/11854555.html)

## 定位

position的属性：

- `absolute` 绝对定位，相对于 `static` 定位以外的第一个父元素进行定位
- `relative` 相对定位，相对于其自身正常位置进行定位
- `fixed` 固定定位，相对于浏览器窗口进行定位
- `static` 默认值。没有定位，元素出现在正常的流中
- `inherit` 规定应该从父元素继承 position 属性的值

CSS3中新增了一个 `position:sticky` 属性，该属性的作用类似 `position:relative` 和 `position:fixed`的结合。元素在设置值之前为相对定位，之后为固定定位。必须指定 top, right, bottom 或 left 四个其中之一，才可使粘性定位生效。

## 自适应

方法一：利用CSS3的`vw`和`vh`单位

```css
.item {
  width: 10vw;
  height: 10vh;
}
```

方法二：利用margin或者padding的百分比，参照父元素的width属性

```css
.item {
	width: 10%;
	padding-bottom: 10%;
	height: 0;
	background: #5091cd;
}
```

## 三角形

方法一：使用`border`生成三角形

```css
.triangle {
  border-color: transparent transparent #f9a541 transparent;
  border-width: 60px;
  border-style: solid;
}
```

方法二： 利用`clip-path`

```css
.triangle {
  /* 将坐标(0,0),(0,80),(80,0)连成一个三角形 */
  clip-path: polygon(0px 0px, 0px 80px, 80px 0px);
  transform: rotate(225deg);
}
```

## CSS3新特性

CSS3 选择器：

- 兄弟选择器（E~F）：选择E元素所有兄弟元素F
- 属性选择器：`E[att^="val"]`、`E[att$="val"]`、`E[att*="val"]`
- 伪类选择器：
	- `E:not(s)`匹配不含有s选择符的元素E
	- `E:root`匹配E元素在文档的根元素
	- `E:last-child`匹配父元素的最后一个子元素E
	- `E:only-child`匹配父元素仅有的一个子元素E
	- `E:nth-child(n)`匹配父元素的第n个子元素E
	- `E:nth-last-child(n)`匹配父元素的倒数第n个子元素E
	- `E:first-of-type`匹配同类型中的第一个同级兄弟元素E
	- `E:last-of-type`匹配同类型中的最后一个同级兄弟元素E
	- `E:only-of-type`匹配同类型中的唯一的一个同级兄弟元素E
	- `E:nth-of-type(n)`匹配同类型中的第n个同级兄弟元素E
	- `E:nth-last-of-type(n)`匹配同类型中的倒数第n个同级兄弟元素E
	- `E:empty`匹配没有任何子元素（包括text节点）的元素E
	- `E:checked`匹配用户界面上处于选中状态的元素E。(用于input type为radio与checkbox)
	- `E:enabled`匹配用户界面上处于可用状态的元素E
	- `E:disabled`匹配用户界面上处于禁用状态的元素E
	- `E:target`匹配相关URL指向的E元素
- 伪元素选择器：
	- `E::first-letter`设置第一个字符的样式
	- `E::first-line`设置第一行的样式
	- `E::selection`设置对象被选择时的颜色
	- `E::placeholder`设置对象文字占位符的样式（input）
	- `E::before`设置在对象前（依据对象树的逻辑结构）发生的内容。用来和content属性一起使用
	- `E::after`设置在对象后（依据对象树的逻辑结构）发生的内容。用来和content属性一起使用

边框：

- `border-radius`设置或检索对象使用圆角边框
- `border-image`：url路径 边框背景图的分割方式 边框厚度 边框背景图的扩展 边框图像的平铺方式

盒子阴影：

- `box-shadow`：水平阴影 垂直阴影 模糊距离 阴影尺寸 阴影颜色  内/外阴影

盒模型：

- `box-sizing`：`content-box`，盒子大小为 `width + padding + border`
- `box-sizing`：`border-box` ， `padding` 和 `border` 是包含到`width`里面的

过渡：

- `transition`：要过渡的属性 + 花费时间 + 运动曲线 + 何时开始

变形：

- `transform`：`translate(x,y) scale(x, y) rotate(deg) skew(deg, deg)`设置变换属性
- `transform-origin: left top;`设置圆点
- `perspective: 300px`透视
- `backface-visibility: visible | hidden;`设置当元素不面向屏幕时是否可见

动画：

- `animation:动画名称 花费时间 运动曲线 何时开始 播放次数 是否反方向;`
- `animation-play-state: paused;`暂停动画
- `animation-fill-mode : none | forwards | backwards | both;`规定动画在播放之前或之后，其动画效果是否可见
- `animation-direction: alternate;`动画应该轮流反向播放
- `animation-iteration-count: infinite;`无限循环播放




文字阴影：

- `text-shadow: 水平位置 垂直位置 模糊距离 阴影颜色;`

背景：

- `background: linear-gradient(渐变的起始位置， 起始颜色， 结束颜色);`线性渐变
- `background: radial-gradient(起始位置, 开始颜色, 中间颜色, 结束颜色);`
- `background-size: x y | contain | cover;`背景缩放
- `background-clip: border-box | padding-box | content-box | text`背景裁剪
- `background-origin: border-box | padding-box | content-box`背景图像参考原点

文本：

- `word-break: normal | keep-all | break-all;`换行方式
- `word-wrap：normal | break-word`单词内部是否允许断行
- `text-overflow：clip | ellipsis`文字溢出处理方式，常与`overflow:hidden;`连用

用户界面：

- `resize：none | both | horizontal | vertical`设置是否允许用户调整元素大小
- `user-select：none | text | all | element`文本是否能被选中

## 其他

1.vertical-align 为什么没有绝对垂直居中？

`vertical-align：baseline | sub | super | top | text-top | middle | bottom | text-bottom | <percentage> | <length>`设置或检索内联元素在行框内的垂直对其方式，适用于内联级与 table-cell 元素。

`vertical-align:middle` 只对行内元素生效，不对块元素生效，即使设置了`display：inline-block`，但对象的确呈内联元素，但内容还是呈块元素展示，所以需要转换成`table`。

```html
<!-- 方法一，直接设置成table -->
<div id="parent"><div id="child"></div></div>
<!--
#parent{
  display:table-cell;
  vertical-align:middle
}
-->

<!-- 方法二，连个子盒子形成参照物，相互设置vertical-align，参照的盒子高度要设置100% -->
<div id="wapper">
  <div id="box"></div>
  <div id="box2"></div>
</div>
<!--
#box {
  display: inline-block;
  vertical-align: middle;
}
#box2 {
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
-->
```

参考文章：

- [“寒冬”三年经验前端面试总结（含头条、百度、饿了么、滴滴等）之CSS篇](https://juejin.im/post/5da32d43e51d45781d5e4bdf)
- [web前端面试总结(自认为还算全面哈哈哈哈哈！！！！）](https://juejin.im/post/5dafb263f265da5b9b80244d)

