# jQeury

1.页面加载事件：

```
    $(window).load(function () {  // 页面中所有元素内容加载完毕后执行
       console.log("hello world!");
    });
    $(document).ready(function () {  // 页面基本的标签加载后执行
       console.log("hei hei");
    });
    jQuery(function () {
        console.log("ha ha");
    });
    $(function () {
        console.log("en en");
    });   // "hei hei" -> "ha ha" -> "en en" -> "hello world!"
```

2.DOM 对象和 jQuery 对象转换：

```
<button id="btn">按钮</button>

var btnObj = document.getElementById("btn");
$(btnObj).click(function(){  // DOM -> jQuery
    $(this).css("backgroundColor", "red");
    });

var btnObj = $("#btn").get(0);
var btnObj = $("#btn")[0];  // jQuery -> DOM
```

3.选择器

```
$("#btn")  // id
$("div")  // 标签
$(".cls")  // 类
$("*")  // 所有的
$("p,div,span,li")  // 并集
$("li.cls")  // 交集
$("#dv li")  // 后代
$("#ul>li")  // 子代
$("uu>li:evevn")  //偶数
$("uu>li:odd")  // 奇数
$("uu>li:eq(4)")  // 索引等于4
$("uu>li:gt(4)")  // 索引大于4
$("uu>li:lt(4)")  // 索引小于4

var index = $(this).index()  // 获取索引
$("#center>li:eq("+index+")").siblings("li").hide();  // 兄弟节点
$("#center>li:eq("+index+")").show();  // 显示

$(this).next().show();  // 下一个
$(this).nextAll().show();  // 后面的所有兄弟元素
$(this).prev().show();  // 前一个
$(this).prevAll().show();  // 前面所有兄弟元素
$(this).children().show();
$(this).parent().show();

$("p").find("span").css('color','red');  // 所有段落中的后代 span 元素
```

4.文本

```
$("#btn").html()  // innerHTML
$("#dv").html("")  // 清空内容
$("#dv").empty()  // 情况元素中的内容
$("#dv").remove()  // 移除 dv 元素
$("#btn").text()  // innerText 或 textContent
$("#btn").val()  // value，获取内容
$("#btn").val("text")  // 设置 value

$("#select").val(4);  // 下拉框第 4 个被选中，selected

$(this).css("backgroundColor","red")  // 属性值写法
$(this).css({"width":"300px","height":"300px"})  // 键值对写法
$(this).css("fontSize","30px").css("color","blue")  // 链式写法
```

5.样式

```
$("#dv").addClass("cls")  // cls 是类名
$("#dv").addClass("cls cls2")

$("#dv").removeClass("cls")  // 移除 cls 类样式
$("#dv").removeClass()  // 移除所有类样式

$("#dv").hasClass("cls")  // 是否有 cls 类样式

$("#dv").toggleClass("cls")  // 切换 cls 类样式
```

6.链式编程

```
$("#dv").css("backgroundColor","red").html(); // 前提返回的是对象
$(this).click(function(){}).mouseover(function(){}).mouseout(function(){})
$(this).preAll().css("color","red").end.nextAll().css("backgroundColor","pink");
```

7.显示隐藏

```
$(this).children("ul").show()
$(this).children("ul").show("normal")
$(this).children("ul").show("fast")
$(this).children("ul").show("slow")
$(this).children("ul").hide();
$(this).children("ul").hide(1000);  // 1s
$(this).children("ul").hide(500,callback);
$(this).children("ul").hide(800,function(){
    $(this).prev().hiden(800,arguments.callee);  // arguments.callee 相当于递归
    });
```

8.滑入滑出/淡入淡出

```
$(this).slideUp();  // 滑入
$(this).slideDown();  // 滑出
$(this).slideToggle();  // 切换，用法和show/hide一样

$(this).fadeIn()  // 淡入
$(this).fadeOut()  // 淡出
$(this).fadeToggle()  // 切换

$(this).fadeTo(1000,0.3)  // 1s 透明度变为 0.3
```

9.animate

```
$(this).animate({"width":"500px"},1000,callback)

$(this).children("ul").stop().show(500);
$(this).children("ul").stop().hide(500);
```

10.创建元素

```
$("div").html("<a herf="http://www.baidu.com">百度</a>");

var a = $("<a herf="http://www.baidu.com">百度</a>");

var a = $("div1").children().clone(); // 克隆

$("div").append(a);
$("div").prepend(a);
$("div").after(a);
$("div").before(a);
a.appendTo($("div"))
$("#dv2").apepend($("#dv1 p"));  // 把 dv1 中的 p 移动到 dv2 中
```

11.自定定义属性 和 设置或返回被选元素的属性和值

```
var aObj = $("<a></a>")
aObj.attr("title","标题")
aObj.attr("herf","http://www.baidu.com")
aObj.text("链接")
aObj.attr("herf")  // 获取href

$("#rd").attr("checked")  // 获取单选按钮 checked
$("#rd").attr("checked",false)
$("#rd").attr("checked",true)

$("#dv :checkbox").prop("checked", true)  // 多选框全选
$("#dv :checkbox").prop("checked", false)  // 多选框全不选
$x.prop("color","FF0000");  // 设置属性值
$(selector).prop("checked")  // 获取属性值

// 区别
<input id="check1" type="checkbox" checked="checked">
$("input").attr('checked')  // checked
$("input").prop('checked')  // true
```

12.获取设置

```
var width = $("div").css("width")  // 100px
var height = $("div").css("height")  // 100px

$("div").css("width",parseInt(width)*2 + "px");
$("div").css("height",parseInt(height)*2 + "px");

$("div").width()  // 100
$("div").height()  // 100
$("div").width(200)  // 设置
$("div").height("200px")  

$("div").offset().left;  // 获取 left top
$("div").offset().top;
$("div").offset({"left":100,"top":100});  // 设置会脱离文档流，默认relative

$("div").scrollLeft()  // 获取卷曲的值
$("div").scrollTop()
```

13.绑定事件

- bind，绑定多个事件，参数：{“事件类型”：函数，...}
- delegate，参数：父级元素.delegate(“子级元素”，“事件类型“，函数)
- on，参数：父级元素.on(”事件类型“，”子级元素“，函数)

```
$("#btn").bind("click",function(){  })  // 绑定事件
$("#btn").bind({"click":function(){}, "mouseover":function(){}, "mouseout":function(){}})  // 绑定多个事件
$("#btn").bind("mouseover mouseout", function(){  })  // 多个事件指向一个函数

$("#dv").delegate("p", "click", function(){ })  // 为div中的p绑定事件

$("#dv").on("click",function(){ })  // 为div绑定事件
$("#dv").on("click","p",function(){ })  // 为div里的p绑定事件
```

14.解绑事件

```
$("#btn1").on("click",function(){ })
$("#btn2").on("click",function(){
    #("#btn1").off("click");  // 取消btn1的点击事件
    })  // 如果存在事件冒泡，父级元素取消事件，子级元素不会取消，需要手动设置
$("div").off("click","**")  // 只解除子级元素的事件绑定
$("div").off()  // 子级元素和父级元素全部解绑

$("#btn1").bind("click",function(){ })
$("#btn2").bind("click",function(){ 
    $("#btn1").unbind("click");  // 取消btn1的点击事件
    })

$("div").delegate("p",click",function(){ })
$("div").undelegate("p",click")  // 取消div里面的p的绑定事件
// 注意：通过delegate绑定的事件，父级元素使用off解绑事件，子级元素也会解绑相同事件
```

15.触发事件

```
$("btn1").click(function(){ })
$("btn2").click(function(){ 
 $("btn1").click()  // 法一：直接调用
 $("btn1").trigger("click")  // 法二
 $("btn1").triggerHandler("click")  // 法三
 })

// 文本框获取焦点
$("#txt").focus()   
$("#txt").trigger("focus")   // 和第一种一样会触发浏览器默认行为
$("#txt").triggerHandler("focus")  // 不会触发浏览器默认行为
```

16.事件对象

```
<div><input type="text"></div>
$("div").on("click","input",function(e){
        console.log(e);
    })

delegateTarget: div  ---- 代码绑定事件的对象
currentTarget: input  ---- 绑定事件的对象
target: input   ---- 真正触发事件的对象
```

17.取消事件冒泡

```
return false;  // 还会取消默认的事件，如超链接的默认的点击事件
```

18.each

```
$("li").each(function(index, ele){  // index 表示索引，0开始
    var op = (index + 1)/10;
    $(ele).css("opacity", op);
    })
```

19.释放$对象控制权

```
var xy = $.noConflict();  // xy变成了$
```

20.ajax

```
$.ajax({
  type: "GET",
  url: "some.php?name=John&location=Boston",
  dataType:"json",
  success: function(msg){
    alert( "Data Saved: " + msg );
  }
});

$.ajax({
   type: "POST",
   url: "some.php",
   data: "name=John&location=Boston", // 传输的数据，GET也可以使用
   dataType:"json", // 预期服务器返回数据
   success: function(msg){
     alert( "Data Saved: " + msg );
   },
   error: function(data){
     console.dir(data);
     $("#info").html("服务器发生错误，请与管理员联系。");
   }
});
```

21.jsonp

```
    $.ajax({
        type:"GET",
        url:"http://test.com/jsonp.php",
        // 使用jsonp方式，默认会在error中输出
        // 除非指定后端接收函数名$foo=$_GET["callback"]，默认会传入一个函数
        dataType:"jsonp",  
        // foo 在一个jsonp请求中重写回调函数的名字
        // 不设置默认会发送callback=213vb...，修改了就是foo=213vb...
        jsonp:"foo",
        // 为jsonp请求指定一个回调函数名,修改后就是foo=foo
        jsonpCallback:"foo"
        success:function (data) {
            console.log(data);
        },
        error:function(data){  
            console.log(data);
        }
    })

    <?php
        $foo = $_GET["foo"];
        echo $foo.'('.json_encode($arr).')';
    ?>
```
