> 今日鸡汤：买得起自己喜欢的东西，去得了自己想去的地方，不会因为身边人的来或走损失生活的质量，反而会因为花自己的钱，来得更有底气一些，这就是应该更努力的原因。

## jQuery 简介

jQuery 是一个 JavaScript 函数库，封装的 js 代码。jQuery 是一个轻量级的"写的少，做的多"的 JavaScript 库。jQuery库包含以下功能：
* HTML 元素选取
* HTML 元素操作
* CSS 操作
* HTML 事件函数
* JavaScript 特效和动画
* HTML DOM 遍历和修改
* AJAX
* Utilities   
* 除此之外，Jquery还提供了大量的插件。

从 [jquery.com](http://jquery.com/) 下载 jQuery 库，jQeury 有两个版本：
* Production version - 用于实际的网站中，已被精简和压缩，文件后缀带 min 的
* Development version - 用于测试和开发（未压缩，是可读的代码）

jQuery 的兼容性很好，但是 2.x 3.x 版本不支持 IE6-8，想兼容低版本浏览器，比如 IE 6-8，Opera 12.X，Safari 5.1+，需要下载 [ jQuery 1.12](https://code.jquery.com/jquery/#jquery-all-1.x) 。

## jQuery 使用
jQuery 语法是通过选取 HTML 元素，并对选取的元素执行某些操作。
基础语法： ```$(selector).action()```
* 美元符号定义 jQuery，打印 `$` 得到 `ƒ ( selector, context )...`，证明 $ 是一个函数，使用的时候需要有`()`
* 选择符（selector）"查询"和"查找" HTML 元素，比如 `$(document)`
* jQuery 的 action() 执行对元素的操作，比如 `$(document).ready();`
```javascript
window.onload = function() {
    //  这个是 js 中，页面加载事件的写法，页面加载完成后才执行
};
$(document).ready(function(){
    //  这个是 jQuery 页面加载事件的写法
	// 把 DOM 对象转换成 jQuery 对象
});
//    两个事件都写，可以看到 jQuery 的时间更先执行， js 的后执行
//    $ === jQuery ，也就是能用 $ 的地方，完全可以使用 jQuery
$(function () {
    //  这个是 jQuery 事件加载函数的另一种写法
});
```

### jQuery 对象与 DOM 最想之间的转换
DOM 对象：使用 JavaScript 中的方法获取页面中的元素返回的对象就是 DOM 对象。DOM 对象只可以使用 DOM 对象的方法和属性。
jQuery 对象：jQuery 对象就是使用 jQuery 的方法获取页面的元素返回的对象就是 jQuery 对象。jQuery 对象只能使用 jQuery 对象的方法。
```jQuery 对象其实就是 DOM 对象的包装集（包含了 DOM 对象的集合（伪数组）），有人把 jQuery 和 DOM 的关系 比喻成洗衣机和衣服的关系，通过洗衣机可以把洗衣机里的衣服都解决掉。```
jQuery 对象和 DOM 对象的相互转换：
1. jQuery 对象转 DOM 对象：
```javascript
    var $li = $("li");   //  第一种方法，把 DOM li 对象 转为 jQuery 对象
	$li[0]   // 即可使用 DOM 的方法，因为 DOM、jQuery 对象是一个伪数组
	
	$li.get(0);    // 第二种 DOM 对象转为 jQuery 对象的方法
```
2. DOM 对象转 jQuery 对象
```javascript
var $obj = $(domObj);  
$(document).ready(function() {   });  //  就是典型的 DOM 对象转 jQuery
```

### jQuery 选择器
jQuery 选择器允许您对 HTML 元素组或单个元素进行操作。
jQuery 选择器基于元素的 id、类、类型、属性、属性值等"查找"（或选择）HTML 元素。 它基于已经存在的 CSS 选择器，除此之外，它还有一些自定义的选择器。也就是和 CSS 差不多。
jQuery 中所有选择器都以美元符号开头：$()。

#### 基本选择器

|  选择器   |  概述   |  备注   |
| --- | --- | --- |
|  $("#id")   |   根据指定的 ID 匹配一个元素  |  ID 选择器   |
|  $("div")   |  选取所有指定的元素   |  元素选择器   |
|   $(".clss")  |  选取包含指定类名的所有元素   |   类选择器  |
|  $("*")   |  选取所有元素   |  通配符选择器   |
|  $(this)  |  选取当前操作对象 HTML 元素  |  对象选择  |
|  $("div1,div2,p")  |  将每一个选择器匹配到的元素合并后一起返回  |  并集选择器  |
|  $("p.intro")  |  选取 class 为 intro 的 p 元素  |  交集选择器，元素既叫 p 也叫 intro  |

#### 层级选择器

|  选择器   |  概述   |  备注   |
| --- | --- | --- |
|  $("father son")  |  在给定的祖先元素下匹配所有的后代元素  |  后代选择器，相当于方法 find，$(“ul”).find(“li”);  |
| $("father>son")   |  在给定的父元素下匹配所有的子元素  |  子元素选择器  |
|  $("prev+next")  |  匹配所有紧接在 prev 元素后的 next 元素  |    |
|  $("prev~siblings")  |  匹配 prev 元素之后的所有 siblings 元素  |   |
| 类似方法  |   |   |
| $(“li”).next()  | 找下一个兄弟  |   |
| $(“li”).prev()  | 找上一次兄弟  |   |
| $(“#first”).parent();  | 查找父亲  |   |
| $(“ul”).children(“li”) | 相当于$(“ul>li”)，子类选择器 |  |
| $(“ul”).find(“li”);  | 相当于$(“ul li”)，后代选择器  |   |
| $(“#first”).siblings(“li”);  | 查找兄弟节点，不包括自己本身  |   |
| $(“li”).eq(2);  | 相当于$(“li:eq(2)”),index从0开始  |   |

#### 子元素选择器

|  选择器   |  概述   |  备注   |
| --- | --- | --- |
|  $("li:first")  |  选取第一个 li 元素  |  伪类选择器  |
|  $("ul li:first-child")  |  选取每个 ul 元素的第一个 li 元素  |    |
|  $("ul li:last-child")   |  选取每个 ul 元素的最后一个 li 元素  |    |
| $('li:last')   |  获取最后一个元素  |    |
|  $("ul li:nth-child(N)")  |  匹配其父元素下的第 N 个子或奇偶元素  |  even、odd  |
|  $("tr:even")  |  匹配所有索引值为偶数的元素，从 0 开始计数  |  表格的1、3...行  |
| $("tr:odd")   |  匹配所有索引值为奇数的元素，从 0 开始计数  |  表格的2、4...行  |
|  $("tr:eq(1)")  |  匹配一个给定索引值的元素， 从 0 开始计数   |  |
|  $("tr:gt(0)")  |  匹配所有大于给定索引值的元素， 从 0 开始计数   |    |
|  $("tr:lt(2)")  |  匹配所有小于给定索引值的元素， 从 0 开始计数   |    |

#### 属性表单选择器

|  选择器   |  概述   |  备注   |
| --- | --- | --- |
|  $("div[id]")  | 匹配包含给定属性的元素  |  有 id 属性的  |
| $("input[name='newsletter']") |  匹配给定的属性是某个特定值的元素  |    |
| $("a[target!='_blank']") | 选取所有 target 属性值不等于 blank 的 a 元素  |    |
| $("input[name^='news']") |  匹配给定的属性是以某些值开始的元素  |    |
|  $("input[name$='letter']") |  匹配给定的属性是以某些值结尾的元素  |    |
|  $(":input")  |  匹配所有 input, textarea, select 和 button 元素  |  表单选择器  |
|  $(":button")  |  匹配所有按钮  |  表单选择器  |
|  $("input:enabled")  |  匹配所有可用元素  |  没有 disabled  |
|  $("input:disabled")  |  匹配所有不可用元素  |    |
|  $("input:checked")  | 匹配所有选中的被选中元素(复选框、单选框等，不包括select中的option)   |    |
| $("select option:selected")   |  匹配所有选中的option元素  |    |

### jQuery 筛选方法

|  方法   |   概述  |   备注  |
| --- | --- | --- |
|  $("p").eq(1)   |   获取第N个元素  |  类似 $("p:eq(1)")   |
|  $(this).hasClass("protected")    |   检查当前的元素是否含有某个特定的类，如果有，则返回true  |  这其实就是 is("." + class)   |
|  $(this).is(expr|obj|ele|fn)   |  根据选择器、DOM元素或 jQuery 对象来检测匹配元素集合，如果其中至少有一个元素符合这个给定的表达式就返回true  |  String|object|Expression|Function   |
|   $(this).map(callback)  |  将一组元素转换成其他数组（不论是否是元素数组）   |     |
|  $(this).filter(expr|obj|ele|fn)   |  筛选出与指定表达式匹配的元素集合   |  String|object|Expression|Function   |
|  $(this).slice(start, [end])  |  选取一个匹配的子集  |  与原来的slice方法类似  |
|  $("div").children()  |  取得一个包含匹配的元素集合中每一个元素的所有子元素的元素集合  |  children([expr])  |
|  $("p").parent()  |  取得一个包含着所有匹配元素的唯一父元素的元素集合  |  parents([expr])  |
|  $("div").siblings()  |  取得一个包含匹配的元素集合中每一个元素的所有唯一同辈元素的元素集合，除自己  |  siblings([expr])  |
|  $("p").find("span")  |  搜索所有与指定表达式匹配的元素  |  与$("p span")相同  |
|  $("p").next()  |  取得一个包含匹配的元素集合中每一个元素紧邻的后面同辈元素的元素集合  |  next([expr])  |
|  $("p").prev()  |  取得一个包含匹配的元素集合中每一个元素紧邻的前一个同辈元素的元素集合  |    |
| $("p").find("span").end()  | 选取所有的p元素，查找并选取span子元素，然后再回过来选取p元素  |   |

### CSS 操作

#### css

1.$(this).css(name|pro|[,val|fn]);
* name ：要访问的属性名称，或是  一个或多个CSS属性组成的一个数组
* properties：要设置为样式属性的名/值对
* name,value：属性名,属性值
* name,function(index, value) ：
	* 1:属性名
	* 2:此函数返回要设置的属性值。接受两个参数，index为元素在对象集合中的索引位置，value是原先的属性值
```javascript
// css(name)  获取想要的样式
$("li").eq(0).css("color");

//   css(name, value)  设置 CSS 样式
$("p").css("color", "red").css("backgroundColor", "pink").css("fontSize", "32px");

// css(obj)  修改多个样式
$("li").css({backgroundColor: "pink",  color: "red",   fontSize: "32px"});

// css(name, 回调函数)
$("li").css("fontSize", function (index,value) {  return parseInt(value) * 2;  });
```

#### 位置

1.var offset = $("p:first").offset([coordinates]);
* 获取匹配元素在当前视口的相对偏移,此方法只对可见元素有效。
* 返回的对象包含两个整型属性：top 和 left，以像素计
* coordinates{top,left} 必需。规定以像素计的 top 和 left 坐标,可能的值如下：
	* 值对，比如 {top:100,left:0} 
	* 带有 top 和 left 属性的对象 
* function(index,coords)  规定返回被选元素新偏移坐标的函数:
	* index - 可选。接受选择器的 index 位置 
	* oldvalue - 可选。接受选择器的当前坐标 
```javascript
//  获取 offset 的值，包含 margin 
var p = $("p:last");
var offset = p.offset();
p.html( "left: " + offset.left + ", top: " + offset.top );  //  <p>left: 0, top: 35</p>

// 设置 offset 的值
p.offset({left: 40, top: 50});  // 值中是不带单位的
```
2.position()  
* 获取匹配元素相对父元素的偏移
* 返回的对象包含两个整型属性：top 和 left ，此方法只对可见元素有效。
```javascript
var p = $("p:first");
var position = p.position();
p.html( "left: " + position.left + ", top: " + position.top );
```
3.scrollTop([val])
* 获取匹配元素相对滚动条顶部的偏移
* 此方法对可见和隐藏元素均有效

4.scrollLeft([val])
* 获取匹配元素相对滚动条左侧的偏移
* 此方法对可见和隐藏元素均有效
```javascript
var p = $("p:first");
$("p:last").text( "scrollTop:" + p.scrollTop() );
$("p:last").text( "scrollLeft:" + p.scrollLeft() );
// 添加参数就是设置滚动条值
```

#### 尺寸

![img_jquerydim](./images/img_jquerydim.gif)
1.height([val|fn])
* 取得匹配元素当前计算的高度值（px）
* 在 jQuery 1.2 以后可以用来获取 window 和 document 的高
* val ：设定CSS中 'height' 的值，可以是字符串或者数字，还可以是一个函数，返回要设置的数值
* function(index, height) ：返回用于设置高度的一个函数。接收元素的索引位置和元素旧的高度值作为参数

2.width([val|fn])
* 取得第一个匹配元素当前计算的宽度值（px），与 height 用法一样
```javascript
$("p").height();  // 获取 height ，不包括 border、padding
$("p").height(20);  // 把所有段落的高设为 20
$("p").height(function (index,value) { return value+10; });  // 每个 p 增加 10 像素

$("p").width();  // 获取第一段的宽
$("p").width(20);  //  把所有段落的宽设为 20:
```
3.innerHeight()
* 获取第一个匹配元素内部区域高度（包括 padding、不包括边框）

4.innerWidth()
* 获取第一个匹配元素内部区域宽度（包括 padding、不包括边框）
```javascript
var p = $("p:first");
p.text( "innerHeight:" + p.innerHeight() ); // 获取第一段落内部区域高度
var p = $("p:last");
p.text( "innerWidth:" + p.innerWidth() ); // 获取最后一段落内部区域宽度
```
5.outerHeight([options])
* 获取第一个匹配元素外部高度（默认包括 padding 和边框）
* options ：Boolean 值，默认为 false。设置为 true 时，计算外边距在内。

6.outerWidth([options])
* 获取第一个匹配元素外部宽度（默认包括补白和边框）。
```javascript
var p = $("p:first");
p.text( "outerHeight:" + p.outerHeight() + " , outerHeight(true):" + p.outerHeight(true) ); // 获取第一段落外部高度，包含和不包含外边距的
p.text( "outerWidth:" + p.outerWidth() + " , outerWidth(true):" + p.outerWidth(true) );
// 获取第一段落外部宽度
```

### 属性操作

#### 属性
1.attr(name|properties|key,value|fn)
* 设置或返回被选元素的属性值，和 css() 方法类似
* name ：属性名称
* properties ：作为属性的“名/值对”对象
* key,value ：属性名称，属性值
* key,function(index, attr) ：
	* 1:属性名称。
	* 2:返回属性值的函数,第一个参数为当前元素的索引值，第二个参数为原先的属性值。
```javascript
$("img").attr("src"); // 返回文档中所有图像的src属性值
$("img").attr({ src: "test.jpg", alt: "Test Image" });  //  为所有图像设置src和alt属性
$("img").attr("src","test.jpg");  //  为所有图像设置src属性
$("img").attr("title", function() { return this.src });  // 把src属性的值设置为title属性的值
```
2.removeAttr(name)
* 从每一个匹配的元素中删除一个属性
* 1.6以下版本在IE6使用JQuery的removeAttr方法删除disabled是无效的。解决的方法就是使用$("XX").prop("disabled",false);1.7版本在IE6下已支持删除disabled
* name ：要删除的属性名
```javascript
$("img").removeAttr("src");  //  将文档中图像的src属性删除
```
3.prop(name|properties|key,value|fn)
* 获取在匹配的元素集中的第一个元素的属性值
* 随着一些内置属性的DOM元素或window对象，如果试图将删除该属性，浏览器可能会产生错误。jQuery第一次分配undefined值的属性，而忽略了浏览器生成的任何错误
* 对于布尔类型的属性，不要attr方法，应该用prop方法，prop用法跟attr方法一样
* name ：属性名称
* properties ：作为属性的“名/值对”对象
* key,value ：属性名称，属性值
* key,function(index, attr)：
	* 1:属性名称
	* 2:返回属性值的函数,第一个参数为当前元素的索引值，第二个参数为原先的属性值
```javascript
$("input[type='checkbox']").prop("checked");  // 选中复选框为true，没选中为false
$("input[type='checkbox']").prop({
  disabled: true
});  // 禁用页面上的所有复选框
$("input[type='checkbox']").prop("disabled", false);
$("input[type='checkbox']").prop("checked", true); // 禁用和选中所有页面上的复选框
$("input[type='checkbox']").prop("checked", function( i, val ) {
  return !val;
});  //  通过函数来设置所有页面上的复选框被选中
```
对于HTML元素本身就带有的固有属性，在处理时，使用prop方法;
对于HTML元素我们自己自定义的DOM属性，在处理时，使用attr方法;
具有 true 和 false 两个属性的属性，如 checked, selected 或者 disabled 使用prop()。

4.removeProp(name)
* 用来删除由.prop()方法设置的属性集
* propertyName ：要删除的属性名
```javascript
var $p = $("p");
$p.prop("luggageCode", 1234);
$p.append("The secret luggage code is: ", String($p.prop("luggageCode")), ". ");
$p.removeProp("luggageCode");
$p.append("Now the secret luggage code is: ", String($p.prop("luggageCode")), ". ");
```

#### CSS 类
1.addClass(class|fn)
* 为每个匹配的元素添加指定的类名
* class ：一个或多个要添加到元素中的CSS类名，请用空格分开
* function(index, class) ：此函数必须返回一个或多个空格分隔的class名。接受两个参数，index参数为对象在这个集合中的索引值，class参数为这个对象原先的class属性值
```javascript
$("p").addClass("selected");
$("p").addClass("selected1 selected2"); // 为匹配的元素加上 'selected' 类

$('ul li:last').addClass(function() {
  return 'item-' + $(this).index();
});   // 给li加上不同的class
```
2.removeClass([class|fn])
* 从所有匹配的元素中删除全部或者指定的类
* class ：一个或多个要删除的CSS类名，请用空格分开
* function(index, class) ：此函数必须返回一个或多个空格分隔的class名。接受两个参数，index参数为对象在这个集合中的索引值，class参数为这个对象原先的class属性值
```javascript
$("p").removeClass("selected"); // 从匹配的元素中删除 'selected' 类

$("p").removeClass(); // 删除匹配元素的所有类

$('li:last').removeClass(function() {
    return $(this).prev().attr('class');
});  //  删除最后一个元素上与前面重复的class 
```
3.toggleClass(class|fn[,sw])
* 如果存在（不存在）就删除（添加）一个类
* class,switch ：1:要切换的CSS类名； 2:用于决定元素是否包含class的布尔值。
* switch ：用于决定元素是否包含class的布尔值
* function(index, class,switch)[, switch] ：
	* 1:用来返回在匹配的元素集合中的每个元素上用来切换的样式类名的一个函数。接收元素的索引位置和元素旧的样式类作为参数。
	* 2: 一个用来判断样式类添加还是移除的 boolean 值。
```javascript
$("p").toggleClass("selected"); // 为匹配的元素切换 'selected' 类

  var count = 0;
  $("p").click(function(){
      $(this).toggleClass("highlight", count++ % 3 == 0);
  });  // 每点击三下加上一次 'highlight' 类，参数class,switch 描述

$('div.foo').toggleClass(function()) {
  if ($(this).parent().is('.bar') {
    return 'happy';
  } else {
    return 'sad';
  }
});  // 根据父元素来设置class属性
```

#### HTML 代码 / 文本 / 值
1.html([val|fn])
* 取得第一个匹配元素的html内容。这个函数不能用于XML文档。但可以用于XHTML文档。在一个 HTML 文档中, 我们可以使用 .html() 方法来获取任意一个元素的内容。 如果选择器匹配多于一个的元素，那么只有第一个匹配元素的 HTML 内容会被获取。
* val ：用于设定HTML内容的值
* function(index, html) ：此函数返回一个HTML字符串。接受两个参数，index为元素在集合中的索引位置，html为原先的HTML值。
```javascript
$('p').html();  // 返回p元素的内容

$("p").html("Hello <b>world</b>!"); // 设置所有 p 元素的内容

$("p").html(function(n){
    return "这个 p 元素的 index 是：" + n;
});  // 使用函数来设置所有匹配元素的内容
```
2.text([val|fn])
* 取得所有匹配元素的内容。结果是由所有匹配元素包含的文本内容组合起来的文本。这个方法对HTML和XML文档都有效。
* val : 用于设置元素内容的文本
* function(index, text) ：此函数返回一个字符串。接受两个参数，index为元素在集合中的索引位置，text为原先的text值。
```javascript
$('p').text();  // 返回p元素的文本内容。

$("p").text("Hello world!");  // 设置所有 p 元素的文本内容

$("p").text(function(n){
    return "这个 p 元素的 index 是：" + n;
});  // 使用函数来设置所有匹配元素的文本内容。
```
3.val([val|fn|arr])
* 设置或返回表单字段的值，在 jQuery 1.2 中,可以返回任意元素的值了。包括select。如果多选，将返回一个数组，其包含所选的值。
* val ：要设置的值
* function(index, value) ：此函数返回一个要设置的值。接受两个参数，index为元素在集合中的索引位置，text为原先的text值
* array ：用于 check/select 的值
```javascript
$("input").val();  // 获取文本框中的值

$("input").val("hello world!");  //  设定文本框的值

$('input:text.items').val(function() {
  return this.value + ' ' + this.className;
});  // 设定文本框的值

$("#single").val("Single2");
$("#multiple").val(["Multiple2", "Multiple3"]);
$("input").val(["check2", "radio1"]);  //  设定一个select和一个多选的select的值
```

### 事件

#### jQuery 事件机制
JavaScript中已经学习过了事件，但是jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

事件发展 ：简单事件绑定 >> bind事件绑定 >> delegate事件绑定 >> on事件绑定

1.bind(type,[data],fn)
* 为每个匹配元素的特定事件绑定事件处理函数
* type,[data],function(eventObject) ：
	* type: 含有一个或多个事件类型的字符串，由空格分隔多个事件。比如"click"或"submit"，还可以是自定义事件名。
	* data:作为event.data属性值传递给事件对象的额外数据对象
	* fn:绑定到每个匹配元素的事件上面的处理函数
* type,[data],false ：
	* type:含有一个或多个事件类型的字符串，由空格分隔多个事件。比如"click"或"submit"，还可以是自定义事件名。
	* data:作为event.data属性值传递给事件对象的额外数据对象
	* false: 将第三个参数设置为false会使默认的动作失效
* events ：一个或多个事件类型的字符串和函数的数据映射来执行他们。
```javascript
$('#foo').bind('mouseenter mouseleave', function() {
  $(this).toggleClass('entered');
});  //  同时绑定多个事件类型

$("button").bind({
  click:function(){$("p").slideToggle();},
  mouseover:function(){$("body").css("background-color","red");},  
  mouseout:function(){$("body").css("background-color","#FFFFFF");}  
});  // 同时绑定多个事件类型/处理程序

function handler(event) {
  alert(event.data.foo);
}
$("p").bind("click", {foo: "bar"}, handler); // 在事件处理之前传递一些附加的数据

$("form").bind("submit", function() { return false; }); // 通过返回false来取消默认的行为并阻止事件冒泡
$("form").bind("submit", function(event){
  event.preventDefault();
}); // 通过使用 preventDefault() 方法只取消默认的行为
$("form").bind("submit", function(event){
  event.stopPropagation();
}); // 通过使用 stopPropagation() 方法只阻止一个事件冒泡
```
2.delegate(selector,[type],[data],fn)
* 指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。
* selector,[type],fn ：
	* selector:选择器字符串，用于过滤器触发事件的元素。
	* type:附加到元素的一个或多个事件。 由空格分隔多个事件值。必须是有效的事件。
	* fn:当事件发生时运行的函数
* selector,[type],[data],fn ：
	* selector:选择器字符串，用于过滤器触发事件的元素。
	* type:附加到元素的一个或多个事件。由空格分隔多个事件值。必须是有效的事件
	* data:传递到函数的额外数据
	* fn:当事件发生时运行的函数
* selector,events ：
	* selector:选择器字符串，用于过滤器触发事件的元素
	* events:一个或多个事件类型的字符串和函数的数据映射来执行他们
```javascript
$("div").delegate("button","click",function(){
  $("p").slideToggle();
}); // 当点击鼠标时，隐藏或显示 p 元素：

$("table").delegate("td", "hover", function(){    
   $(this).toggleClass("hover");
});  // delegate这个方法可作为live()方法的替代，使得每次事件绑定到特定的DOM元素
$("table").each(function(){    
   $("td", this).live("hover", function(){          
      $(this).toggleClass("hover");   
   });    
});
```
3.on(events,[selector],[data],fn)
* 在选择元素上绑定一个或多个事件的事件处理函数
* events,[selector],[data],fn ：
	* events:一个或多个用空格分隔的事件类型和可选的命名空间，如"click"或"keydown.myPlugin" 
	* selector:一个选择器字符串用于过滤器的触发事件的选择器元素的后代。如果选择的< null或省略，当它到达选定的元素，事件总是触发
	* data:当一个事件被触发时要传递event.data给事件处理函数
	* fn:该事件被触发时执行的函数。 false 值也可以做一个函数的简写，返回false
* events-map,[selector],[data] :
	* events-map:个用字符串表示的，一个或多个空格分隔的事件类型和可选的命名空间，值表示事件绑定的处理函数
	* selector:一个选择器字符串过滤选定的元素，该选择器的后裔元素将调用处理程序。如果选择是空或被忽略，当它到达选定的元素，事件总是触发
	* data:当一个事件被触发时要传递event.data给事件处理函数
```javascript
function myHandler(event) {
alert(event.data.foo);
}
$("p").on("click", {foo: "bar"}, myHandler);

$("form").on("submit", false);
$("form").on("submit", function(event) {
  event.preventDefault();
});
$("form").on("submit", function(event) {
  event.stopPropagation();
});  //  取消事件冒泡

// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
$(selector).on( "click",“span”, function() {});
```

#### 触发事件与事件解绑
1.unbind(type,[data|fn]])
* bind()的反向操作，从每一个匹配的元素中删除绑定的事件
* type,[fn] ：
	* type:删除元素的一个或多个事件,由空格分隔多个事件值。
	* fn:要从每个匹配元素的事件中反绑定的事件处理函数
* type,false ：
	* type:删除元素的一个或多个事件,由空格分隔多个事件值
	* false:设置为false会使默认的动作失效
* eventObj ：事件对象。这个 eventObj 参数来自事件绑定函数

2.undelegate([selector,[type],fn])
* 删除由 delegate() 方法添加的一个或多个事件处理程序

3.off(events,[selector],[fn])
* 在选择元素上移除一个或多个事件的事件处理函数
```javascript
$(selector).unbind(); //解绑所有的事件
$(selector).unbind("click"); //解绑指定的事件

$( selector ).undelegate(); //解绑所有的delegate事件
$( selector).undelegate( “click” ); //解绑所有的click事件

$(selector).off();  // 解绑匹配元素的所有事件
$(selector).off("click");  // // 解绑匹配元素的所有click事件
// 一般使用 off 
```

1.trigger(type,[data])
* 在每一个匹配的元素上触发某类事件
* type,[data] ：
	* type:一个事件对象或者要触发的事件类型
	* data:传递给事件处理函数的附加参数
* event ：事件发生时运行的函数
```javascript
$(selector).click(); //触发 click事件
$(selector).trigger("click");

$("p").click( function (event, a, b) {
  // 一个普通的点击事件时，a和b是undefined类型
  // 如果用下面的语句触发，那么a指向"foo",而b指向"bar"
} ).trigger("click", ["foo", "bar"]);
```

#### 事件对象
```javascript
//screenX和screenY	对应屏幕最左上角的值
//clientX和clientY	距离页面左上角的位置（忽视滚动条）
//pageX和pageY	距离页面最顶部的左上角的位置（会计算滚动条的距离）

//event.keyCode	按下的键盘代码
//event.data	存储绑定事件时传递的附加数据

//event.stopPropagation()	阻止事件冒泡行为
//event.preventDefault()	阻止浏览器默认行为
//return false:既能阻止事件冒泡，又能阻止浏览器默认行为。
```

#### 常用事件

|  事件   |  概述   |   备注  |
| --- | --- | --- |
|  blur([[data],fn])   |  当元素失去焦点时触发 blur 事件   |  $("p").blur( function () { alert("Hello World!"); } );   |
|  click([[data],fn])   |  触发每一个匹配元素的click事件   |  $("p").click( function () { $(this).hide(); });   |
|  dblclick([[data],fn])   |   当双击元素时，会发生 dblclick 事件  |  $("p").dblclick( function () { alert("Hello World!"); });   |
|  focus([[data],fn])   |  当元素获得焦点时，触发 focus 事件   |   $("#login").focus();   |
|  keydown([[data],fn])   |   当键盘或按钮被按下时，发生 keydown 事件  |  $(window).keydown(function(event){  switch(event.keyCode) {   // 不同的按键可以做不同的事情   不同的浏览器的keycode不同}  });   |
|  keypress([[data],fn])   |  当键盘或按钮被按下时，发生 keypress 事件   |  $("input").keypress(function(){  $("span").text(i+=1);});   |
|  keyup([[data],fn])   |   当按钮被松开时，发生 keyup 事件。它发生在当前获得焦点的元素上  |   $("input").keyup(function(){  $("input").css("background-color","#D6D6FF");
});  |
|  mousedown([[data],fn])   |  当鼠标指针移动到元素上方，并按下鼠标按键时，会发生 mousedown 事件   |  $("button").mousedown(function(){  $("p").slideToggle(); });   |
|   mouseenter([[data],fn])  |  当鼠标指针穿过元素时，会发生 mouseenter 事件。该事件大多数时候会与mouseleave 事件一起使用   |  $("p").mouseenter(function(){  $("p").css("background-color","yellow"); });   |
|  mouseleave([[data],fn])   |  当鼠标指针离开元素时，会发生 mouseleave 事件。该事件大多数时候会与mouseenter 事件一起使用   |  $("p").mouseleave(function(){  $("p").css("background-color","#E9E9E4"); });   |
|  mousemove([[data],fn])   |  当鼠标指针在指定的元素中移动时，就会发生 mousemove 事件   |  $(document).mousemove(function(e){ $("span").text(e.pageX + ", " + e.pageY); });   |
|   mouseout([[data],fn])  |  当鼠标指针从元素上移开时，发生 mouseout 事件   |  $("p").mouseout(function(){  $("p").css("background-color","#E9E9E4"); });   |
|  mouseover([[data],fn])   |  当鼠标指针位于元素上方时，会发生 mouseover 事件，```与mouseenter```   | $("p").mouseover(function(){  $("p").css("background-color","yellow"); });    |
|  mouseup([[data],fn])   |  当在元素上放松鼠标按钮时，会发生 mouseup 事件   |  $("button").mouseup(function(){  $("p").slideToggle(); });   |
|  resize([[data],fn])   |  当调整浏览器窗口的大小时，发生 resize 事件   |  $(window).resize(function() {  $('span').text(x+=1); });   |
|  scroll([[data],fn])   |  当用户滚动指定的元素时，会发生 scroll 事件   |  $(window).scroll( function() {  ...do something...  } );   |
|  select([[data],fn])   |   当 textarea 或文本类型的 input 元素中的文本被选择时，会发生 select 事件  |  $(":text").select( function () {  ...do something... } );   |
|  submit([[data],fn])   |  当提交表单时，会发生 submit 事件   |  $("form").submit( function () {  return false; } );   |
|  unload([[data],fn])   |  在当用户离开页面时，会发生 unload 事件   |  $(window).unload( function () { alert("Bye now!"); } );   |

#### 文档处理

|   方法  |   概述  |  备注   |
| --- | --- | --- |
|  append(content|fn)   |  向每个匹配的元素内部追加内容   |  $("p").append("<b>Hello</b>");   |
|  appendTo(content)   |  把所有匹配的元素追加到另一个指定的元素元素集合中，追加到父节点   |  $("p").appendTo("div");   |
|  prepend(content)   |  向每个匹配的元素内部前置内容  |  $("p").prepend("<b>Hello</b>");   |
|  prependTo(content)   |  把所有匹配的元素前置到另一个、指定的元素元素集合中   |  $("p").prependTo("#foo");   |
|  after(content|fn)   |  在每个匹配的元素之后插入内容   |  $("p").after("<b>Hello</b>");   |
|  before(content|fn)   |  在每个匹配的元素之前插入内容   |  $("p").before("<b>Hello</b>");   |
|  replaceWith(content|fn)   |  将所有匹配的元素替换成指定的HTML或DOM元素，是移动到目标位置来替换，而不是复制一份来替换。   |  $("p").replaceWith("<b>Paragraph. </b>");   |
|  empty()   |  删除匹配的元素集合中所有的子节点，清空内容   |  $("p").empty();   |
|  remove([expr])   |   从DOM中删除所有匹配的元素，删除元素  |  $("p").remove();   |
|  clone([Even[,deepEven]])   |   克隆匹配的DOM元素并且选中这些克隆的副本  |  $("b").clone().prependTo("p");   |

#### 动画效果

|  方法名   |  概述   |  备注   |
| --- | --- | --- |
|   show([speed,[easing],[fn]])  |  显示隐藏的匹配元素；speed:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)；easing:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"   |  $("p").show()   |
|  hide([speed,[easing],[fn]])   |   隐藏显示的元素  |  $("p").hide("fast",function(){   alert("Animation Done."); });   |
|  slideDown([speed],[easing],[fn])   |   通过高度变化（向下增大）来动态地显示所有匹配的元素，在显示完成后可选地触发一个回调函数  |   $("p").slideDown("slow");  |
|  slideUp([speed,[easing],[fn]])   |  通过高度变化（向上减小）来动态地隐藏所有匹配的元素，在隐藏完成后可选地触发一个回调函数   |  $("p").slideUp("slow");   |
|   slideToggle([speed],[easing],[fn])  |   通过高度变化来切换所有匹配元素的可见性，并在切换完成后可选地触发一个回调函数  |   $("p").slideToggle("slow");  |
|  fadeIn([speed],[easing],[fn])   |  通过不透明度的变化来实现所有匹配元素的淡入效果，并在动画完成后可选地触发一个回调函数   |   $("p").fadeIn("slow");  |
|  fadeOut([speed],[easing],[fn])   |  通过不透明度的变化来实现所有匹配元素的淡出效果，并在动画完成后可选地触发一个回调函数   |  $("p").fadeOut("slow");   |
|  fadeToggle([speed,[easing],[fn]])   |   通过不透明度的变化来开关所有匹配元素的淡入和淡出效果，并在动画完成后可选地触发一个回调函数  |   $("p").fadeToggle("slow","linear");  |
|  animate(params,[speed],[easing],[fn])   |  用于创建自定义动画的函数；params:一组包含作为动画属性和终值的样式属性和及其值的集合   |    $("#block").animate({  width: "90%",  height: "100%",  fontSize: "10em", borderWidth: 10 }, 1000 );  |
|  stop([clearQueue],[jumpToEnd])   |  停止所有在指定元素上正在运行的动画；clearQueue:如果设置成true，则清空队列，可以立即结束动画；gotoEnd:让当前正在执行的动画立即完成，并且重设show和hide的原始样式，调用回调函数等；queue:用来停止动画的队列名称   |  $("#stop").click(function(){  $("#box").stop(); });   |
| delay(duration,[queueName])  | 设置一个延时来推迟执行队列中之后的项目;duration:延时时间，单位：毫秒；queueName:队列名词，默认是Fx，动画队列  | $('#foo').slideUp(300).delay(800).fadeIn(400);  |

### 其它核心内容

|  方法   |  概述   |  备注   |
| --- | --- | --- |
|  each(callback)   |  以每一个匹配的元素作为上下文来执行一个函数；参数一表示当前元素在所有匹配元素中的索引号； 参数二表示当前元素（DOM对象）   |  $(selector).each(function(index,element){});   |
|  jQuery.noConflict([extreme])   |  运行这个函数将变量$的控制权让渡给第一个实现它的那个库，避免命名冲突   |  var c = $.noConflict();//释放$的控制权,并且把$的能力给了c   |

### 常用插件
1.jquery.color.js ：animate不支持颜色的渐变，但是使用了jquery.color.js后，就可以支持颜色的渐变了

使用步骤：
1. 引入jQuery文件
2. 引入插件（如果有用到css的话，需要引入css）
3. 使用插件

2.jquery.lazyload.js ：懒加载插件；比如首页图片只加载一个页面那么多，向下滑动的时候再加载其它的。

3.jquery.ui.js ：jQueryUI 专指由 jQuery 官方维护的 UI 方向的插件
[官方 API](http://api.jqueryui.com/category/all/)
[菜鸟教程](http://www.runoob.com/jqueryui/jqueryui-tutorial.html)

4.自定义插件
给jquery对象增加一个新的方法，让jquery对象拥有某一个功能。
```javascript
//通过给$.fn添加方法就能够扩展jquery对象
$.fn. pluginName = function() {};
```
## To Be Continue ...