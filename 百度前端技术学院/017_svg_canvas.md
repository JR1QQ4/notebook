## 数据可视化

1.数据可视化技术
- 数据空间：是由n维属性和m个元素组成的数据集所构成的多维信息空间
- 数据开发：是指利用一定的算法和工具对数据进行定量的推演和计算；
- 数据分析：指对多维数据进行切片、块、旋转等动作剖析数据，从而能多角度多侧面观察数据；
- 数据可视化：是指将大型数据集中的数据以图形图像形式表示，并利用数据分析和开发工具发现其中未知信息的处理过程。
- 应用：报表类；BI分析工具；

2.Echarts
（1）坐标轴：X轴、Y轴，X轴和Y轴都由轴线、刻度、刻度标签、轴标题四个部分组成。
- X轴：常用来标示数据的维度，维度一般用来指数据的类别，是观察数据的角度，例如“销售时间” “销售地点” “产品名称”等。
    + 轴线：建议显示；
    + 刻度：轴线下方，建议显示；
    + 隔线：建议显示；
    + 标记文字：轴线下方，居中对齐，建议显示；
    + 标记文字显示方式：水平，垂直，斜角；
    + 轴名称：显示可选，位置可自定义；

- Y轴：常常用来标示数据的数值，数值是用来具体考察某一类数据的数量值，也是我们需要分析的指标。例如“销售数量”和“销售金额”等。
    + 轴线：显示可选；
    + 刻度：显示可选；
    + 隔线：建议显示；
    + 标记文字：轴线内外可选，建议显示；
    + 轴名称：显示可选，位置可自定义；

(2)可视化色彩理论基础
a.色相：色彩的相貌和特征。自然界中色彩的种类很多，色相指色彩的种类和名称。如；红、橙、黄、绿、青、蓝、紫等等颜色的种类变化就叫色相。

b.明度 指色彩的亮度。颜色有深浅、明暗的变化。比如，深黄、中黄、淡黄、柠檬黄等黄色在明度上就不一样。这些颜色在明暗、深浅上的不同变化，也就是色彩的又一重要特征一一明度变化。
- 不同色相之间的明度变化。如：白比黄亮、黄比橙亮、橙比红亮、红比紫亮、紫比黑亮；
- 在某种颜色中加白色，亮度就会逐渐提高，加黑色亮度就会变暗，但同时它们的纯度(颜色的饱和度)就会降低

c.饱和度 色彩的鲜艳程度，饱和度越高,表现越鲜明,饱和度较低,表现则较黯淡。

## SVG

1.SVG是XML语言的一种形式，有点类似XHTML，它可以用来绘制矢量图形。SVG可以通过定义必要的线和形状来创建一个图形，也可以修改已有的位图，或者将这两种方式结合起来创建图形。图形和其组成部分可以变形，可以合成，还可以通过滤镜完全改变外观。

2.HTML中的SVG：SVG 文件可通过以下标签嵌入 HTML 文档：`<embed>`、`<object>` 或者 `<iframe>`
```
// pluginspage 属性指向下载插件的 URL
<embed src="rect.svg" width="300" height="100" 
type="image/svg+xml"
pluginspage="http://www.adobe.com/svg/viewer/install/" />

// codebase 属性指向下载插件的 URL
<object data="rect.svg" width="300" height="100" 
type="image/svg+xml"
codebase="http://www.adobe.com/svg/viewer/install/" />

<iframe src="rect.svg" width="300" height="100">
</iframe>

// 引用 SVG 的命名空间
<html xmlns:svg="http://www.w3.org/2000/svg">
<body>
<p>This is an HTML paragraph</p>
<svg:svg width="300" height="100" version="1.1" >
<svg:circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red" />
</svg:svg>
</body>
</html>
```

3.SVG 形状
- 矩形 `<rect>`
- 圆形 `<circle>`
- 椭圆 `<ellipse>`
- 线 `<line>`
- 折线 `<polyline>`
- 多边形 `<polygon>`
- 路径 `<path>`
```
// rx 和 ry 属性可使矩形产生圆角
<rect x="20" y="20" rx="20" ry="20" width="250"
height="100" style="fill:red;stroke:black;
stroke-width:5;opacity:0.5"/>

// cx 和 cy 属性定义圆点的 x 和 y 坐标，r 属性定义圆的半径
<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>

// cx 和 cy 属性定义圆点的 x 和 y 坐标，rx 和 ry 属性定义水平、垂直半径
<ellipse cx="300" cy="150" rx="200" ry="80"
style="fill:rgb(200,100,50);
stroke:rgb(0,0,100);stroke-width:2"/>

// x1 和 y1 属性在 x 和 y 轴定义线条的开始，x2 和 y2 属性在 x 和 y 轴定义线条的开始
<line x1="0" y1="0" x2="300" y2="300"
style="stroke:rgb(99,99,99);stroke-width:2"/>

// points 属性定义多边形每个角的 x 和 y 坐标
<polygon points="220,100 300,210 170,250 123,234"
style="fill:#cccccc;
stroke:#000000;stroke-width:1"/>

// 折线，fill:white才能看出是折线
<polyline points="0,0 0,20 20,20 20,40 40,40 40,60"
style="fill:white;stroke:red;stroke-width:2"/>

// 开始于 250 150，到达 150 350，然后从那里开始到 350 350，最后在 250 150 关闭路径。
// M = moveto(M X,Y) ：将画笔移动到指定的坐标位置
// L = lineto(L X,Y) ：画直线到指定的坐标位置
// H = horizontal lineto(H X)：画水平线到指定的X坐标位置
// V = vertical lineto(V Y)：画垂直线到指定的Y坐标位置
// C = curveto(C X1,Y1,X2,Y2,ENDX,ENDY)：三次贝赛曲线
// S = smooth curveto(S X2,Y2,ENDX,ENDY)
// Q = quadratic Belzier curve(Q X,Y,ENDX,ENDY)：二次贝赛曲线
// T = smooth quadratic Belzier curveto(T ENDX,ENDY)：映射，简写的贝塞尔曲线
// A = elliptical Arc(A RX,RY,XROTATION,FLAG1,FLAG2,X,Y)：弧线
// Z = closepath()：关闭路径
// 大写字母，表示采用绝对定位。另一种是用小写字母，表示采用相对定位
<path d="M250 150 L150 350 L350 350 Z" />
```

4.SVG 滤镜
- feBlend
- feColorMatrix
- feComponentTransfer
- feComposite
- feConvolveMatrix
- feDiffuseLighting
- feDisplacementMap
- feFlood
- feGaussianBlur
- feImage
- feMerge
- feMorphology
- feOffset
- feSpecularLighting
- feTile
- feTurbulence
- feDistantLight
- fePointLight
- feSpotLight

5.高斯模糊：必须在 `<defs>` 标签中定义 SVG 滤镜。<filter> 标签用来定义 SVG 滤镜。<filter> 标签必须嵌套在 <defs> 标签内。
```
<defs>
// 同一滤镜可被文档中的多个元素使用
<filter id="Gaussian_Blur">
// 滤镜效果是通过 <feGaussianBlur> 标签进行定义的。fe 后缀可用于所有的滤镜
// <feGaussianBlur> 标签的 stdDeviation 属性可定义模糊的程度
// in="SourceGraphic" 这个部分定义了由整个图像创建效果
<feGaussianBlur in="SourceGraphic" stdDeviation="3" />
</filter>
</defs>

// filter:url 属性用来把元素链接到滤镜。当链接滤镜 id 时，必须使用 # 字符
<ellipse cx="200" cy="150" rx="70" ry="40"
style="fill:#ff0000;stroke:#000000;
stroke-width:2;filter:url(#Gaussian_Blur)"/>
```

6.渐变：SVG 渐变必须在 `<defs>` 标签中进行定义。有两种主要的渐变类型：线性渐变、放射性渐变。
（1）线性渐变，`<linearGradient>` 可用来定义 SVG 的线性渐变，必须嵌套在 `<defs>` 的内部。线性渐变可被定义为水平、垂直或角形的渐变：
-  当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
-  当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
-  当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变
```
<defs>
// <linearGradient> 标签的 id 属性可为渐变定义一个唯一的名称
// <linearGradient> 标签的 x1、x2、y1、y2 属性可定义渐变的开始和结束位置
// 属性：spreadMethod="pad"、"repeat"、"reflect"
<linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
// 渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个 <stop> 标签来规定。
// offset 属性用来定义渐变的开始和结束位置。
<stop offset="0%" style="stop-color:rgb(255,255,0);
stop-opacity:1"/>
<stop offset="100%" style="stop-color:rgb(255,0,0);
stop-opacity:1"/>
</linearGradient>
</defs>

// fill:url(#orange_red) 属性把 ellipse 元素链接到此渐变
<ellipse cx="200" cy="190" rx="85" ry="55"
style="fill:url(#orange_red)"/>
```

（2）放射性渐变：`<radialGradient>` 用来定义放射性渐变，必须嵌套在 `<defs>` 中。
```
// cx、cy 和 r 属性定义外圈， fx 和 fy 定义内圈
<radialGradient id="grey_blue" cx="50%" cy="50%" r="50%"
fx="50%" fy="50%">
<stop offset="0%" style="stop-color:rgb(200,200,200);
stop-opacity:0"/>
<stop offset="100%" style="stop-color:rgb(0,0,255);
stop-opacity:1"/>
</radialGradient>
</defs>

// fill:url(#grey_blue) 属性把 ellipse 元素链接到此渐变
<ellipse cx="230" cy="200" rx="110" ry="100"
style="fill:url(#grey_blue)"/>
```

7.绘制流程
```
<svg version="1.1"
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="red" />
  <circle cx="150" cy="100" r="80" fill="green" />
  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>
</svg>

1.从svg根元素开始：应舍弃来自 (X)HTML的doctype声明，属性version和属性baseProfile属性是必不可少的，作为XML的一种方言，SVG必须正确的绑定命名空间 （在xmlns属性中绑定）。

2.绘制一个完全覆盖图像区域的矩形 <rect/>，把背景颜色设为红色。

3.一个半径80px的绿色圆圈<circle/>绘制在红色矩形的正中央 （向右偏移150px，向下偏移100px）。

4.绘制文字“SVG”。文字被填充为白色， 通过设置居中的锚点把文字定位到期望的位置：在这种情况下，中心点应该对应于绿色圆圈的中点。还可以精细调整字体大小和垂直位置，确保最后的样式是美观的。
```

8.基本属性
- 元素的渲染顺序：SVG文件全局有效的规则是“后来居上”，越后面的元素越可见。
- svg文件可以直接在浏览器上展示，或者通过以下几种方法嵌入到HTML文件中：
    + 如果HTML是XHTML并且声明类型为application/xhtml+xml，可以直接把SVG嵌入到XML源码中。
    + 如果HTML是HTML5并且浏览器支持HTML5，同样可以直接嵌入SVG。然而为了符合HTML5标准，可能需要做一些语法调整。
    + 可以通过 object 元素引用SVG文件：`<object data="image.svg" type="image/svg+xml" />`
    + 也可以使用 iframe 元素引用SVG文件：`<iframe src="image.svg"></iframe>`
    + 理论上同样可以使用 img 元素，但是在低于4.0版本的Firefox 中不起作用。
    + 最后SVG可以通过JavaScript动态创建并注入到HTML DOM中。 

9.文件类型:普通SVG文件是包含SVG标记的简单文本文件。推荐使用“.svg”（全部小写）作为此类文件的扩展名。由于在某些应用（比如地图应用等）中使用时，SVG文件可能会很大，SVG标准同样允许gzip压缩的SVG文件。推荐使用“.svgz”（全部小写）作为此类文件扩展名 。

9.坐标定位：在 SVG 文档中的1个像素对应输出设备（比如显示屏）上的1个像素。但是这种情况是可以改变的，否则 SVG 的名字里也不至于会有“Scalable”（可缩放）这个词。如同CSS可以定义字体的绝对大小和相对大小，SVG也可以定义绝对大小（比如使用“pt”或“cm”标识维度）同时SVG也能使用相对大小，只需给出数字，不标明单位，输出时就会采用用户的单位。用户单位和屏幕单位的映射关系被称为用户坐标系统。

10.填充和边框
（1）Fill 和 Stroke 属性
```
// 用直边结束线段，它是常规做法，线段边界90度垂直于描边的方向、贯穿它的终点
stroke-linecap="butt"  
// 效果差不多，但是会稍微超出实际路径的范围，超出的大小由stroke-width控制。
stroke-linecap="square"  
// 边框的终点是圆角，圆角的半径也是由stroke-width控制的。
stroke-linecap="round"  

// stroke-linejoin属性，用来控制两条描边线段之间，用什么方式连接。
stroke-linejoin="miter"  // 用方形画笔在连接处形成尖角
stroke-linejoin="round"  // 用圆角连接，实现平滑效果
stroke-linejoin="bevel"  // 连接处会形成一个斜接

// 将虚线类型应用在描边上
// 第一个用来表示填色区域的长度，第二个用来表示非填色区域的长度。
stroke-dasharray="5,5"
```

（2）使用CSS
-  上色和填充的部分一般是可以用CSS来设置的，比如fill，stroke，stroke-dasharray等，
-  不包括渐变和图案等功能
```
<rect x="10" height="180" y="10" width="180" style="stroke: black; fill: red;"/>

<?xml version="1.0" standalone="no"?>
// 外链式 #MyRect {  fill: red; stroke: black; }
<?xml-stylesheet type="text/css" href="style.css"?>
<svg width="200" height="150" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect height="10" width="10" id="MyRect"/>
</svg>
```

11.图案：patterns（图案）是SVG中用到的最让人混淆的填充类型之一。
```
<?xml version="1.0" standalone="no"?>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="Gradient1">
      <stop offset="5%" stop-color="white"/>
      <stop offset="95%" stop-color="blue"/>
    </linearGradient>
    <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
      <stop offset="5%" stop-color="red"/>
      <stop offset="95%" stop-color="orange"/>
    </linearGradient>

    <pattern id="Pattern" x="0" y="0" width=".25" height=".25">
      <rect x="0" y="0" width="50" height="50" fill="skyblue"/>
      <rect x="0" y="0" width="25" height="25" fill="url(#Gradient2)"/>
      <circle cx="25" cy="25" r="20" fill="url(#Gradient1)" fill-opacity="0.5"/>
    </pattern>
  </defs>

  <rect fill="url(#Pattern)" stroke="black" x="0" y="0" width="200" height="200"/>
</svg>
```

12.Texts：在SVG中有两种截然不同的文本模式. 一种是写在图像中的文本，另一种是SVG字体。
```
// 属性x和属性y性决定了文本在视口中显示的位置。
// 属性text-anchor：start、middle、end或inherit，决定从这一点开始的文本流的方向
// 设置字体属性：font-系列、font-variant、font-stretch、font-size-adjust、kerning、letter-spacing、word-spacing和text-decoration
<text x="10" y="10">Hello World!</text>

<font id="Font1" horiz-adv-x="1000">
  <font-face font-family="Super Sans" font-weight="bold" font-style="normal"
      units-per-em="1000" cap-height="600" x-height="400"
      ascent="700" descent="300"
      alphabetic="0" mathematical="350" ideographic="400" hanging="500">
    <font-face-src>
      <font-face-name name="Super Sans Bold"/>
    </font-face-src>
  </font-face>
  <missing-glyph><path d="M0,0h200v200h-200z"/></missing-glyph>
  <glyph unicode="!" horiz-adv-x="300"><!-- Outline of exclam. pt. glyph --></glyph>
  <glyph unicode="@"><!-- Outline of @ glyph --></glyph>
  <!-- more glyphs -->
</font>

<font>
  <font-face font-family="Super Sans" />
  <!-- and so on -->
</font>
<text font-family="Super Sans">My text uses Super Sans</text>
```

其它文本相关的元素：`<tspan></tspan>`、`<tref></tref>`、`<textPath></textPath>`

13.基础变形
```
// 元素g是用来组合对象的容器，可以把属性赋给一整个元素集合
<g fill="red">
  <rect x="0" y="0" width="10" height="10" />
  <rect x="20" y="0" width="10" height="10" />
</g>
```

（1）平移
```
// 移到点(30,40)，如果没有指定第二个值，它默认被赋值0。
<rect x="0" y="0" width="10" height="10" transform="translate(30,40)" />
```

（2）旋转
```
<rect x="20" y="20" width="20" height="20" transform="rotate(45)" />
```

（3）斜切：利用一个矩形制作一个斜菱形。可用skewX()变形和skewY()变形。

（4）缩放：scale()变形改变了元素的尺寸。它需要两个数字，作为比率计算如何缩放。0.5表示收缩到50%。如果第二个数字被忽略了，它默认等于第一个值。

14.剪切和遮罩
-  Clipping用来移除在别处定义的元素的部分内容。在这里，任何半透明效果都是不行的。它只能要么显示要么不显示。
-  Masking允许使用透明度和灰度值遮罩计算得的软边缘。
```
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <clipPath id="cut-off-bottom">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
  </defs>

  <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
</svg>

<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <linearGradient id="Gradient">
      <stop offset="0" stop-color="white" stop-opacity="0" />
      <stop offset="1" stop-color="white" stop-opacity="1" />
    </linearGradient>
    <mask id="Mask">
      <rect x="0" y="0" width="200" height="200" fill="url(#Gradient)"  />
    </mask>
  </defs>

  <rect x="0" y="0" width="200" height="200" fill="green" />
  <rect x="0" y="0" width="200" height="200" fill="red" mask="url(#Mask)" />
</svg>

// 用opacity定义透明度
<rect x="0" y="0" width="100" height="100" opacity=".5" />
<circle cx="100" cy="100" r="50" stroke="yellow" stroke-width="40" stroke-opacity=".5" fill="red" />
```

15.其它SVG内容
```
// 嵌入光栅图像
<svg version="1.1"
     xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
     width="200" height="200">
  <image x="90" y="-65" width="128" height="146" transform="rotate(45)"
     xlink:href="https://developer.mozilla.org/media/img/mdn-logo.png"/>
</svg>
```

## Canvas

1.<canvas> 元素本身并没有绘制能力（它仅仅是图形的容器） - 您必须使用脚本来完成实际的绘图任务。getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。Canvas 的默认大小为300像素×150像素（宽×高，像素的单位是px）。

2.基本用法
```
<canvas id="tutorial" width="150" height="150"></canvas>

<script>
var canvas = document.getElementById('tutorial');
var ctx = canvas.getContext('2d');
ctx.fillStyle = "rgba(0, 0, 200, 0.5)";
ctx.fillRect (30, 30, 55, 50);
</script>
```

(1)绘制矩形
- fillRect(x, y, width, height)  绘制一个填充的矩形
- strokeRect(x, y, width, height)  绘制一个矩形的边框
- clearRect(x, y, width, height)  清除指定矩形区域，让清除部分完全透明
```
ctx.fillRect(25, 25, 100, 100);
ctx.clearRect(45, 45, 60, 60);
ctx.strokeRect(50, 50, 50, 50);
```

(2)绘制路径:首先，你需要创建路径起始点 -> 然后你使用画图命令去画出路径 -> 之后你把路径封闭 -> 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。
- beginPath() 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径
- closePath() 闭合路径之后图形绘制命令又重新指向到上下文中
- stroke() 通过线条来绘制图形轮廓
- fill() 通过填充路径的内容区域生成实心的图形
```
ctx.beginPath();
ctx.moveTo(75, 50);  // 将笔触移动到指定的坐标x以及y上
ctx.lineTo(100, 75);  // 绘制一条从当前位置到指定x以及y位置的直线
ctx.lineTo(100, 25);
ctx.fill();
```

(3)圆弧
- arc(x, y, radius, startAngle, endAngle, anticlockwise)，以（x,y）为圆心的以radius为半径的圆弧，从startAngle开始到endAngle结束，anticlockwise为true时，是逆时针方向
- arcTo(x1, y1, x2, y2, radius)，根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点
- arc()函数中表示角的单位是弧度，不是角度：弧度=(Math.PI/180)*角度
```
    ctx.beginPath();
    ctx.arc(75,75,50,0,Math.PI*2,true); // 绘制
    ctx.moveTo(110,75);
    ctx.arc(75,75,35,0,Math.PI,false);   // 口(顺时针)
    ctx.moveTo(65,65);
    ctx.arc(60,65,5,0,Math.PI*2,true);  // 左眼
    ctx.moveTo(95,65);
    ctx.arc(90,65,5,0,Math.PI*2,true);  // 右眼
    ctx.stroke();
```

(4)二次贝塞尔曲线及三次贝塞尔曲线
- quadraticCurveTo(cp1x, cp1y, x, y)，绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点
- bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)，绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点
```
 // 二次贝塞尔曲线
 ctx.beginPath();
 ctx.moveTo(75,25);
 ctx.quadraticCurveTo(25,25,25,62.5);
 ctx.quadraticCurveTo(25,100,50,100);
 ctx.quadraticCurveTo(50,120,30,125);
 ctx.quadraticCurveTo(60,120,65,100);
 ctx.quadraticCurveTo(125,100,125,62.5);
 ctx.quadraticCurveTo(125,25,75,25);
 ctx.stroke();

  //三次贝塞尔曲线
 ctx.beginPath();
 ctx.moveTo(75,40);
 ctx.bezierCurveTo(75,37,70,25,50,25);
 ctx.bezierCurveTo(20,25,20,62.5,20,62.5);
 ctx.bezierCurveTo(20,80,40,102,75,120);
 ctx.bezierCurveTo(110,102,130,80,130,62.5);
 ctx.bezierCurveTo(130,62.5,130,25,100,25);
 ctx.bezierCurveTo(85,25,75,37,75,40);
 ctx.fill();
```

(5)矩形
- rect(x, y, width, height)：绘制一个左上角坐标为（x,y），宽高为width以及height的矩形

(6)Path2D 对象
```
new Path2D();     // 空的Path对象
new Path2D(path); // 克隆Path对象
new Path2D(d);    // 从SVG建立Path对象

// 添加了一条路径到当前路径（可能添加了一个变换矩阵）
Path2D.addPath(path [, transform])​ 

// 使用 SVG paths
var p = new Path2D("M10 10 h 80 v 80 h -80 Z");
```

3.使用样式和颜色
(1)色彩 Colors
- fillStyle = color：设置图形的填充颜色
- strokeStyle = color：设置图形轮廓的颜色
```
// 这些 fillStyle 的值均为 '橙色'
ctx.fillStyle = "orange";
ctx.fillStyle = "#FFA500";
ctx.fillStyle = "rgb(255,165,0)";
ctx.fillStyle = "rgba(255,165,0,1)";
```

(2)透明度 Transparency
- globalAlpha = transparencyValue：有效的值范围是 0.0 （完全透明）到 1.0（完全不透明），默认是 1.0
```
// 指定透明颜色，用于描边和填充样式
ctx.strokeStyle = "rgba(255,0,0,0.5)";
ctx.fillStyle = "rgba(255,0,0,0.5)";
```

(3)线型 Line styles
- lineWidth = value：设置线条宽度
- lineCap = type：设置线条末端样式，butt，round 和 square
- lineJoin = type：设定线条与线条间接合处的样式，round, bevel 和 miter
- miterLimit = value：限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度
- getLineDash()：返回一个包含当前虚线样式，长度为非负偶数的数组
- setLineDash(segments)：设置当前虚线样式
- lineDashOffset = value：设置虚线样式的起始偏移量
```
function draw() {
    var ctx = document.getElementById('canvas').getContext('2d');
    for (var i = 0; i < 10; i++){
        ctx.lineWidth = 1+i;
        ctx.beginPath();
        ctx.moveTo(5+i*14,5);
        ctx.lineTo(5+i*14,140);
        ctx.stroke();
    }
}

ctx.setLineDash([4, 2]);
ctx.lineDashOffset = -offset;
```

(4)渐变 Gradients
- createLinearGradient(x1, y1, x2, y2)：渐变的起点 (x1,y1) 与终点 (x2,y2)
- createRadialGradient(x1, y1, r1, x2, y2, r2)：前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆
- gradient.addColorStop(position, color)：position 参数必须是一个 0.0 与 1.0 之间的数值，表示渐变中颜色所在的相对位置；color 参数必须是一个有效的 CSS 颜色值
```
var lineargradient = ctx.createLinearGradient(0,0,150,150);
var radialgradient = ctx.createRadialGradient(75,75,0,75,75,100);

var lineargradient = ctx.createLinearGradient(0,0,150,150);
lineargradient.addColorStop(0,'white');
lineargradient.addColorStop(1,'black');
```

(5)图案样式 Patterns
- createPattern(image, type)：Image 可以是一个 Image 对象的引用，或者另一个 canvas 对象。Type 必须是下面的字符串值之一：repeat，repeat-x，repeat-y 和 no-repeat
```
var img = new Image();
img.src = 'someimage.png';
var ptrn = ctx.createPattern(img,'repeat');
```

(6)阴影 Shadows
- shadowOffsetX = float：shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离
- shadowOffsetY = float：负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0
- shadowBlur = float：shadowBlur 用于设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵的影响，默认为 0
- shadowColor = color：shadowColor 是标准的 CSS 颜色值，用于设定阴影颜色效果，默认是全透明的黑色
```
    ctx.shadowOffsetX = 2;
    ctx.shadowOffsetY = 2;
    ctx.shadowBlur = 2;
    ctx.shadowColor = "rgba(0, 0, 0, 0.5)";
    ctx.font = "20px Times New Roman";
    ctx.fillStyle = "Black";
    ctx.fillText("Sample String", 5, 30);
```

(7)Canvas 填充规则
-  "nonzero":non-zero winding rule, 默认值.
-   "evenodd":  even-odd winding rule.
```
    var ctx = document.getElementById('canvas').getContext('2d'); 
    ctx.beginPath(); 
    ctx.arc(50, 50, 30, 0, Math.PI*2, true);
    ctx.arc(50, 50, 15, 0, Math.PI*2, true);
    ctx.fill("evenodd");
```

4.绘制文本
(1)fillText(text, x, y [, maxWidth])：在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的
(2)strokeText(text, x, y [, maxWidth])：在指定的(x,y)位置绘制文本边框，绘制的最大宽度是可选的
```
ctx.fillText("Hello world", 10, 50);
ctx.strokeText("Hello world", 10, 50);
```

(3)有样式的文本
- font = value：默认的字体是 10px sans-serif
- textAlign = value：文本对齐选项，start, end, left, right or center
- textBaseline = value：基线对齐，top, hanging, middle, alphabetic, ideographic, bottom
- direction = value：文本方向，ltr, rtl, inherit

(4)预测量文本宽度
- measureText()：将返回一个 TextMetrics对象的宽度、所在像素，这些体现文本特性的属性
```
    var text = ctx.measureText("foo"); // TextMetrics object
    text.width; // 16;
```

5.使用图像 Using images
(1)获得需要绘制的图片：这些源统一由 CanvasImageSource类型来引用
- HTMLImageElement：这些图片是由Image()函数构造出来的，或者任何的<img>元素
- HTMLVideoElement：用一个HTML的 <video>元素作为你的图片源，可以从视频中抓取当前帧作为一个图像
- HTMLCanvasElement：可以使用另一个 <canvas> 元素作为你的图片源
- ImageBitmap：这是一个高性能的位图，可以低延迟地绘制，它可以从上述的所有源以及其它几种源中生成
```
var img = new Image();   // 创建img元素
img.onload = function(){
  // 执行drawImage语句
  ctx.drawImage(img,0,0);  // 绘制图片

  ctx.drawImage(img,j*50,i*38,50,38); // 缩放 Scaling
}
img.src = 'myImage.png'; // 设置图片源地址
```

（2）切片 Slicing
- drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)，第一个参数和其它的是相同的，都是一个图像或者另一个 canvas 的引用。其它8个参数最好是参照右边的图解，前4个是定义图像源的切片位置和大小，后4个则是定义切片的目标显示位置和大小
```
  ctx.drawImage(document.getElementById('source'),
                33,71,104,124,21,20,87,104);
```

6.变形 Transformations
（1）状态的保存和恢复 Saving and restoring state
- save()：保存画布(canvas)的所有状态
- restore()：save 和 restore 方法是用来保存和恢复 canvas 状态的，都没有参数。Canvas 的状态就是当前画面应用的所有样式和变形的一个快照
- Canvas状态存储在栈中，每当save()方法被调用后，当前的状态就被推送到栈中保存。一个绘画状态包括：
    + 当前应用的变形（即移动，旋转和缩放）
    + strokeStyle, fillStyle, globalAlpha, lineWidth, lineCap, lineJoin, miterLimit, shadowOffsetX, shadowOffsetY, shadowBlur, shadowColor, globalCompositeOperation 的值
    + 当前的裁切路径（clipping path）

（2）移动 Translating
- translate(x, y)：translate 方法接受两个参数。x 是左右偏移量，y 是上下偏移量

（3）旋转 Rotating
- rotate(angle)：只接受一个参数：旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值
- 旋转的中心点始终是 canvas 的原点，如果要改变它，我们需要用到 translate 方法

（4）缩放 Scaling
- scale(x, y)：两个参数都是实数，可以为负数，x 为水平缩放因子，y 为垂直缩放因子，如果比1小，会比缩放图形， 如果比1大会放大图形

（5）变形 Transforms
- transform(m11, m12, m21, m22, dx, dy)：将当前的变形矩阵乘上一个基于自身参数的矩阵
    + m11：水平方向的缩放
    + m12：水平方向的倾斜偏移
    + m21：竖直方向的倾斜偏移
    + m22：竖直方向的缩放
    + dx：水平方向的移动
    + dy：竖直方向的移动
- setTransform(m11, m12, m21, m22, dx, dy)：将当前的变形矩阵重置为单位矩阵，然后用相同的参数调用 transform 方法
- resetTransform()：重置当前变形为单位矩阵，等价于：ctx.setTransform(1, 0, 0, 1, 0, 0);

7.组合 Compositing
（1）globalCompositeOperation：设定了在画新图形时采用的遮盖策略，其值是一个标识12种遮盖方式的字符串
- source-over：这是默认设置，并在现有画布上下文之上绘制新图形
- source-in：新图形只在新图形和目标画布重叠的地方绘制。其他的都是透明的
- source-out：在不与现有画布内容重叠的地方绘制新图形
- source-atop：新图形只在与现有画布内容重叠的地方绘制
- ...

（2）裁切路径
- clip()：将当前正在构建的路径转换为当前的裁剪路径

8.基本的动画
（1）动画的基本步骤
- 清空 canvas：最简单的做法就是用 clearRect 方法。
- 保存 canvas 状态：如果你改变 canvas 状态的设置（样式，变形之类的），又要在每画一帧之时都是原始状态的话
- 绘制动画图形（animated shapes）
- 恢复 canvas 状态

（2）操控动画 Controlling an animation
- setInterval(function, delay)：当设定好间隔时间后，function会定期执行
- setTimeout(function, delay)：在设定好的时间之后执行函数
- requestAnimationFrame(callback)：告诉浏览器你希望执行一个动画，并在重绘之前，请求浏览器执行一个特定的函数来更新动画

9.高级动画
```
// 绘制小球
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
var ball = {
  x: 100,
  y: 100,
  radius: 25,
  color: 'blue',
  draw: function() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, true);
    ctx.closePath();
    ctx.fillStyle = this.color;
    ctx.fill();
  }
};
ball.draw();
```

10.像素操作
（1）ImageData 对象
- width：图片宽度，单位是像素
- height：图片高度，单位是像素、
- data：Uint8ClampedArray类型的一维数组，包含着RGBA格式的整型数据，范围(0,255]
```
// 创建一个ImageData对象
var myImageData = ctx.createImageData(width, height);

// 得到场景像素数据
var myImageData = ctx.getImageData(left, top, width, height);

// 在场景中写入像素数据,dx和dy参数表示在场景内左上角绘制的像素数据的设备坐标
ctx.putImageData(myImageData, dx, dy);
```



