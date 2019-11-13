## 贝塞尔曲线

1.贝塞尔曲线(Bezier curves)是曲率的一种典型代表，在CSS的时间函数(timing function)中就有一个贝塞尔曲线——x轴和y轴的距离用来确定时间。
```
// “立方-贝塞尔”:三次方贝塞尔曲线
ease: cubic-bezier(0.25, 0.1, 0.25, 1.0)
linear: cubic-bezier(0.0, 0.0, 1.0, 1.0)
ease-in: cubic-bezier(0.42, 0, 1.0, 1.0)
ease-out: cubic-bezier(0, 0, 0.58, 1.0)
ease-in-out: cubic-bezier(0.42, 0, 0.58, 1.0)
```

2.一个标准的3次贝塞尔曲线需要4个点：起始点、终止点（也称锚点）以及两个相互分离的中间点。

3.常用的贝塞尔曲线:cubic-bezier (x1,y1,x2,y2)
```
$easeInSine: cubic-bezier(0.47, 0, 0.745, 0.715);
$easeOutSine: cubic-bezier(0.39, 0.575, 0.565, 1);
$easeInOutSine: cubic-bezier(0.445, 0.05, 0.55, 0.95);
$easeInBack: cubic-bezier(0.6, -0.28, 0.735, 0.045);
$easeOutBack: cubic-bezier(0.175, 0.885, 0.32, 1.275);
$easeInOutBack: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

[贝塞尔曲线的一些事情](https://www.w3cplus.com/animation/mathematical-intuition-behind-bezier-curves.html)
[cubic-bezier贝塞尔曲线CSS3动画工具](https://blog.csdn.net/qq_25600055/article/details/51045163)
[贝塞尔曲线与CSS3动画、SVG和canvas的基情](https://www.zhangxinxu.com/wordpress/2013/08/%E8%B4%9D%E5%A1%9E%E5%B0%94%E6%9B%B2%E7%BA%BF-cubic-bezier-css3%E5%8A%A8%E7%94%BB-svg-canvas/)
[JS模拟CSS3动画-贝塞尔曲线](https://www.cnblogs.com/yanan-boke/p/8875571.html)
[css3动画——常用的贝塞尔曲线](https://www.cnblogs.com/yansi/p/4012038.html)
[CSS3 三次贝塞尔曲线(cubic-bezier)](https://blog.csdn.net/zhaozjc112/article/details/52909172)
