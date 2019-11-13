# 移动web

1.像素密度

- 物理像素（physical pixel）:反映的就是显示屏内部led灯的数量
- DPI（Dots Per Inch）打印机每平方英寸可以喷出的墨汁点数
- PPI（Pixel Per Inch）屏幕每平方英寸的物理像素数量
    + 960*640的3.5英寸屏，PPI = （根号下960*960+640*640） / 3.5 = 330
- 像素时一个相对长度单位（像素并没有固定的长度）
- px是viewport像素
- 逻辑像素/点（device point / device pixel / point ）将所有设备根据距离，透视缩放到一个相等水平的观看距离之后得到的尺寸
- dpr （device point ratio / device pixel ratio） 渲染像素与逻辑像素的比例

2.设备独立像素 pt

- 有的1pt = 1px，有的1pt = 2px
- window.devicePixelRatio

3.获取屏幕物理像素尺寸：

- window.screen.width  与  window.screen.height

4.2倍图，用于适应手机宽度。

5.视口viewport，显示内容的，

-  PC端取决于浏览器窗口的大小

```
document.documentElement.clientHeight
document.documentElement.clientWidth
```

-  layout viewport（布局视口）

```
document.documentElement.clientHeight
document.documentElement.clientWidth
```

-  ideal viewport（理想视口）设备屏幕取余

```
window.screen.width
window.screen.height
window.screen.width / window.devicePixelRatio  // 老设备
window.screen.height / window.devicePixelRatio // 老设备
```

-  设置viewport

```
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0,minimum-scale=1, maximum-scale=2.0,user-scalable=yes"/>
">
initial-scale：load初始缩放比例
maximum-scale：允许用户缩放到的最大比例
minimum-scale：允许用户缩放到的最小比例
user-scalable：用户是否可以手动缩放
```

6.触摸

（1）事件

```
touchstart // 触摸开始
touchmove  // 触摸移动
touchend // 手指离开触发
touchcancel  // 意外中断
```

（2）TouchEvent属性

```
touches：当前屏幕所有的手指对象
targetTouches：当前元素上的手指对象
changedTouches：当前屏幕上变换的手指对象--从无到有，从有到无
```

7.拖拽

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Title</title>
    <style>
        body {
            background-color: #ffedcb;
            color: #fff;
            font-size: 4em;
        }
        div {
            width: 100px;
            height: 100px;
            background-image: -webkit-linear-gradient(left, red, purple);
            background-image: linear-gradient(left, red, purple);
            position: absolute;
            top: 10px;
            left: 0;
        }

        #dv2 {
            top: 120px;
            background-image: -webkit-linear-gradient(left, #ff8d00, #ff0044);
            background-image: linear-gradient(left, #ff8d00, #ff0044);
        }
        #dv3 {
            top: 230px;
            background-image: -webkit-linear-gradient(left, #ff8f02, #000eff);
            background-image: linear-gradient(left, #ff8f02, #000eff);
        }
        #dv4 {
            top: 340px;
            background-image: -webkit-linear-gradient(left, #12ff09, #0057ff);
            background-image: linear-gradient(left, #12ff09, #0057ff);
        }
        #dv5 {
            top: 450px;
            background-image: -webkit-linear-gradient(left, #0004ff, #d100ff);
            background-image: linear-gradient(left, #0004ff, #d100ff);
        }
        p {
            width: 100px;
            height: 100px;
            position: absolute;
            right: 20px;
            color: orange;
        }
    </style>
</head>
<body>
<p>移动端拖拽</p>
<div id="dv1">1</div>
<div id="dv2">2</div>
<div id="dv3">3</div>
<div id="dv4">4</div>
<div id="dv5">5</div>
<script>
    var startX, startY, endX, endY;
    document.addEventListener("touchstart", function (e) {
        if (e.target.nodeName == "DIV") {
            startX = e.targetTouches[0].clientX - e.target.offsetLeft;
            startY = e.targetTouches[0].clientY - e.target.offsetTop;
            // 使用 transform 就不能使用 offsetLeft
        }
    })
    document.addEventListener("touchmove", function (e) {
        if (e.target.nodeName == "DIV") {
            endX = e.targetTouches[0].clientX - startX;
            endY = e.targetTouches[0].clientY - startY;
            if (endX < 0) {
                endX = 0;
            } else if (endX > document.documentElement.clientWidth - e.target.offsetWidth) {
                endX = document.documentElement.clientWidth - e.target.offsetWidth;
            }
            if (endY < 0) {
                endY = 0;
            } else if (endY > document.documentElement.clientHeight - e.target.offsetHeight) {
                endY = document.documentElement.clientHeight - e.target.offsetHeight;
            }
            e.target.style.left = endX + "px";
            e.target.style.top = endY + "px";
        }
    })
    document.addEventListener("touchend", function (e) {
        if (e.target.nodeName == "DIV") {
            e.target.style.left = "0";
            if(e.target.innerHTML == "1"){
                e.target.style.top = "0";
            }else if(e.target.innerHTML == "2") {
                e.target.style.top = "120px";
            }else if(e.target.innerHTML == "3") {
                e.target.style.top = "230px";
            }else if(e.target.innerHTML == "4") {
                e.target.style.top = "340px";
            }else if(e.target.innerHTML == "5") {
                e.target.style.top = "450px";
            }
        }
    })
</script>
</body>
</html>
```

9.插件：zepto.js（移动端jq）  iscroll.js（滑动）  fastclick.js（点透）  swiper.js（轮播图） steller.js（视差）

10.jq获取宽度

```
 * width():它只能得到当前元素的内容的宽度
 * innerWidth():它能获取当前元素的内容的宽度+padding
 * outerWidth():获取当前元素的内容的宽度+padding+border
 * outerWidth(true):获取元素的内容的宽度+padding+border+margin
```



# 响应式

1.media媒体查询

(1)使用

```
@media mediatype and|not|only (media featrue) {
    css-code;
}
或者
<link rel="stylesheet" media="mediatype and|not|only (media featrue)" href="mystylesheet.css">

@media screen and (min-width: 768px) and (max-width: 992px) {
    body {
        background-color: orange;
    }
}
```

(2)其中 mediatype 主要包含：

-  all：所有设备
-  print：打印机和打印预览
-  screen：电脑屏幕，平板电脑，智能手机等
-  tv：电视机类型的设备
-  projection：方案展示，投影仪，比如幻灯片
-  speech：屏幕阅读器

(3)media featrue 主要包含：

- device-width/device-height：输出设备的屏幕可见宽高
- max-device-width/max-device-height：屏幕可见最大宽高
    + max-device-width 在pc端缩小浏览器宽度不变
- min-device-width/min-device-height：屏幕可见最小宽高
- max-width/max-height：页面最大可见区域宽高
    + max-width pc端和移动端一致
- min-width/min-height：页面最小可见区域宽高

2.框架：Bootstrap，Amaze UI，Framework7 

3.Bootstrap

（1）IE8 需要 Respond.js 才能实现对媒体查询（media query）
（2）IE 兼容模式：`<meta http-equiv="X-UA-Compatible" content="IE=edge">`
（3）container,container-fluid容器
（4）less：> lessc styles.less styles.css

```
@gray-dark:    lighten(#000, 20%);   // #333
@brand-primary: darken(#428bca, 6.5%); // #337ab7
.masthead {
  background-color: @brand-primary;
}
@alert-message-background: @brand-info;
.alert {
  background-color: @alert-message-background;
}
```

4.rem与em:

```
        html {
            font-size: 14px;
        }
        .box {
            width: 10em;
            height:10em;
            background-color: orange;
            font-size: 12px;
        }
        .layout {
            width: 10rem;
            height:10rem;
            background-color: purple;
            font-size: 12px;
        }

<div class="box"></div>  // 参照当前元素的字号，如果没有设置，参照父容器或浏览器字号
<div class="layout"></div>  //  参照根元素的字号
```

5.将屏幕分成若干份

```
        @media screen and (device-width: 320px) {
            html {
                font-size: 16px;  // 将屏幕分成10份
            }
        }
        @media screen and (device-width: 360px) {
            html {
                font-size: 18px;  // 将屏幕分成10份
            }
        }
        @media screen and (device-width: 375px) {
            html {
                font-size: 18.75px;  // 将屏幕分成10份
            }
        }
        @media screen and (device-width: 414px) {
            html {
                font-size: 20.07px;  // 将屏幕分成10份
            }
        }
        .layout {
            width:20rem;
            height:20rem;
            background-color: orange;
        }

        <div class="layout"></div>
```
