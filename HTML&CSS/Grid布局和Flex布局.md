# Grid布局，还是Flex布局？

网格布局和Flex布局的差异？

有人认为：Flexbox用于一维布局，一行或一列。网格用于二维布局，多行和多列。

有的人认为：网格使用真实的列和行，内容会被一列一列、一行一行的排列。但是Flexbox没有，不仅是在二维里面，而且在一维里面也是如此。Flexbox并不适用于我们一直在使用的大部分功能。

大多数人认为：将Grid用于页面级布局，而将flexbox用于其他所有内容。

先回顾一下网格布局和Flex布局。

## 网格布局

采用网格布局的区域，称为"容器"（container）。容器内部采用网格定位的子元素，称为"项目"（item）。

容器里面的水平区域称为"行"（row），垂直区域称为"列"（column）。

行和列的交叉区域，称为"单元格"（cell）。

划分网格的线，称为"网格线"（grid line）。水平网格线划分出行，垂直网格线划分出列。正常情况下，n行有n + 1根水平网格线，m列有m + 1根垂直网格线，比如三行就有四根水平网格线。

![grid](./images/grid.png)

Grid 布局的属性分成两类。一类定义在容器上面，称为容器属性；另一类定义在项目上面，称为项目属性。

容器属性：

- display 属性：指定一个容器采用网格布局
	- display: grid;  默认情况下，容器元素都是块级元素
	- display: inline-grid;  设成行内元素
- grid-template-columns 属性：定义每一列的列宽
- grid-template-rows 属性：定义每一行的行高
	- 行列除了使用绝对单位，也可以使用百分比
		- grid-template-rows: 100px 100px 100px;
		- grid-template-columns: 33.33% 33.33% 33.33%;
	- repeat() 接受两个参数，第一个参数是重复的次数，第二个参数是所要重复的值
		- grid-template-columns: repeat(3, 33.33%);
		- grid-template-columns: repeat(2, 100px 20px 80px);  定义了6列
	- auto-fill 关键字表示自动填充
		- grid-template-columns: repeat(auto-fill, 100px); 每列宽度100px，然后自动填充，直到容器不能放置更多的列
	- fr 关键字
		- grid-template-columns: 1fr 2fr; 两列的宽度分别为1fr和2fr，就表示后者是前者的两倍
	- minmax()
		- grid-template-columns: 1fr 1fr minmax(100px, 1fr);  列宽不小于100px，不大于1fr
	- auto 关键字表示由浏览器自己决定长度
		- grid-template-columns: 100px auto 100px;
	- 网格线的名称
		- grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4]; 
		- grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4]; 指定每一根网格线的名字
- row-gap 属性设置行与行的间隔（行间距）
- column-gap 属性设置列与列的间隔（列间距）
- gap 属性是grid-column-gap和grid-row-gap的合并简写形式  gap: <row-gap> <column-gap>;
- grid-template-areas 属性用于定义区域
- grid-auto-flow 属性默认值是row，即"先行后列"。设成column，变成"先列后行"。
	- 还可以设成row dense和column dense。row dense，表示"先行后列"，并且尽可能紧密填满，尽量不出现空格
- justify-items 属性设置单元格内容的水平位置（左中右）  justify-items: start | end | center | stretch;
- align-items属性设置单元格内容的垂直位置（上中下）  align-items: start | end | center | stretch;
- place-items属性是align-items属性和justify-items属性的合并简写形式  place-items: <align-items> <justify-items>;
- justify-content属性是整个内容区域在容器里面的水平位置（左中右）
	- justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
- align-content属性是整个内容区域的垂直位置（上中下）
	-  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
- place-content属性是align-content属性和justify-content属性的合并简写形式  place-content: <align-content> <justify-content>
- grid-auto-columns属性和grid-auto-rows属性浏览器自动创建的多余网格的列宽和行高
- grid-template属性是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式
- grid属性是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式

项目属性:

- grid-column-start属性：左边框所在的垂直网格线
- grid-column-end属性：右边框所在的垂直网格线
- grid-row-start属性：上边框所在的水平网格线
- grid-row-end属性：下边框所在的水平网格线
	- grid-column-start: 2; grid-column-end: 4;  第二根垂直网格线，第四根垂直网格线
	- 使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格  grid-column-start: span 2;
- grid-column属性是grid-column-start和grid-column-end的合并简写形式  grid-column: 1 / 3;
- grid-row属性是grid-row-start属性和grid-row-end的合并简写形式  grid-row: 1 / 2;
- grid-area 属性指定项目放在哪一个区域   grid-area: e;
	- grid-area属性还可用作grid-row-start、grid-column-start、grid-row-end、grid-column-end的合并简写形式  
		- grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
- justify-self属性设置单元格内容的水平位置（左中右） justify-self: start | end | center | stretch;
- align-self属性设置单元格内容的垂直位置（上中下） align-self: start | end | center | stretch;
- place-self属性是align-self属性和justify-self属性的合并简写形式  place-self: <align-self> <justify-self>;

[参考示例](http://dongqunren.gitee.io/notebook/interview/blog/grid.html)

## Flex布局

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![flex](./images/flex.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

容器的属性:

- flex-direction属性决定主轴的方向（即项目的排列方向）  flex-direction: row | row-reverse | column | column-reverse;
- flex-wrap属性定义，如果一条轴线排不下，如何换行  flex-wrap: nowrap | wrap | wrap-reverse;
- flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap,  flex-flow: <flex-direction> || <flex-wrap>;
- justify-content属性定义了项目在主轴上的对齐方式  justify-content: flex-start | flex-end | center | space-between | space-around;
- align-items属性定义项目在交叉轴上如何对齐  align-items: flex-start | flex-end | center | baseline | stretch;
- align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用
	- align-content: flex-start | flex-end | center | space-between | space-around | stretch;

项目的属性: 

- order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
- flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
- flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
- flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size），默认值为auto
- flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto，后两个属性可选  flex: none | <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> 
- align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
	- align-self: auto | flex-start | flex-end | center | baseline | stretch;

[参考示例](http://dongqunren.gitee.io/notebook/interview/blog/flex.html)

##  Grid布局，还是Flex布局？

如果你需要使用`calc()`进行布局，此时你可能需要用到Grid布局。

Grid和flexbox之间的最大区别是，Grid使我们能够更好控制二维（行和列）中项目的摆放，而flexbox则不行。同样，这并不意味着您永远不应该将网格用于一维布局。

当我们有9个以上但少于12个的项目时会发生什。我们是否希望新项目像我们已经看到的示例那样仅位于下一行的开头？还是我们希望他们的行为有所不同？也许如果下一行只有一项，我们希望它占用该行的所有可用空间，例如下面的示例A。或者，如果有两个项目，那么我们希望将它们居中，例如示例B。

![to-grid-or-to-flex](./images/to-grid-or-to-flex.png)

使用网格布局和自动放置，我们只能将最后一个项目放置在左侧的单元格中，假设`direction`属性的值未设置为`rtl`（在这种情况下，项目的放置将从右向左流动，最后一项将放置在右侧的单元格中）。Flexbox允许项目弯曲。这意味着我们可以结合使用flex和alignment属性来控制这些项目的行为。

因此，无论您是为上面的布局选择Grid还是flexbox，实际上都取决于您希望网格项目如何工作-以及针对不同情况的不同答案。

如果使用的是Grid，则需要考虑的另一个问题是浏览器支持，我们是否希望在不支持Grid的浏览器（IE11及以下）中显示布局。常用功能查询来满足这些情况。

```css
.grid {
	display: flex;
	flex-wrap: wrap;
	/* Rest of the fallback layout code */
}

@supports (display: grid) {
	.grid {
		display: grid;
		/* Rest of the Grid code */
	}
}
```

但是，如果您发现自己花费了数小时试图为不支持Grid的浏览器复制完全相同的布局，那么首先就没有太多理由使用Grid。Grid的伟大之处在于它可以完成Flexbox本身无法做到的事情。


参考文章：

- [CSS Grid 网格布局教程](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)
- [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
- [Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
- [Flexbox 布局的最简单表单](http://www.ruanyifeng.com/blog/2018/10/flexbox-form.html)
- [To Grid or to Flex?](https://css-irl.info/to-grid-or-to-flex/)