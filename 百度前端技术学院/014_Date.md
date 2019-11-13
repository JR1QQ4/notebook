## 函数

1.内置函数
```
var myText = 'I am a string';
var newString = myText.replace('string', 'sausage');
console.log(newString);
```

2.自定义函数
```
function draw() {
  ctx.clearRect(0,0,WIDTH,HEIGHT);
  for (var i = 0; i < 100; i++) {
    ctx.beginPath();
    ctx.fillStyle = 'rgba(255,0,0,0.5)';
    ctx.arc(random(WIDTH), random(HEIGHT), random(50), 0, 2 * Math.PI);
    ctx.fill();
  }
}

function random(number) {
  return Math.floor(Math.random()*number);
}
```

3.匿名函数
```
var myButton = document.querySelector('button');
myButton.onclick = function() {
  alert('hello');
}
```

4.函数参数，参数有时称为参数，属性（properties）或甚至属性（attributes）。
```
function howManyArgs() {
  alert(arguments.length);
}
```

## Date

1.Date
```
var myDate=new Date(); // Fri Jun 21 2019 15:16:50 GMT+0800 (中国标准时间)
var start = Date.now(); // 1561101463857
var date1 = myDate.getDate(); // 21，1-31
var day1 = myDate.getDay(); // 5，0表示星期天
var day1 = myDate.getFullYear(); // 2019
var day1 = myDate.getHours(); // 15，0-23
var day1 = myDate.getMilliseconds(); // 682，毫秒数
var day1 = myDate.getMinutes(); // 21，分钟数
var day1 = myDate.getMonth(); // 5，0表示第一月
var day1 = myDate.getSeconds(); // 41，秒数
var day1 = myDate.getTime(); // 1561101701682

var event = new Date('August 19, 1975 23:15:30');
event.setDate(24); // Sun Aug 24 1975 23:15:30 GMT+0800 (中国标准时间)
event.setFullYear(1969); // Sun Aug 24 1969 23:15:30 GMT+0800 (中国标准时间)
event.setHours(20); // Sun Aug 24 1969 20:15:30 GMT+0800 (中国标准时间)
event.setMilliseconds(456); // Sun Aug 24 1969 20:15:30 GMT+0800 (中国标准时间)
event.setMinutes(45); // Sun Aug 24 1969 20:45:30 GMT+0800 (中国标准时间)
event.setMonth(3); // Thu Apr 24 1969 20:45:30 GMT+0800 (中国标准时间)
event.setSeconds(42); // Thu Apr 24 1969 20:45:42 GMT+0800 (中国标准时间)
var jsonDate = event.toJSON(); // "1969-04-24T12:45:42.456Z"
```

## 定时器

1.定时器
```
window.setTimeout(function, milliseconds);
window.clearTimeout(timeoutVariable);

<button onclick="setTimeout(myFunction, 3000)">试一试</button>
<button onclick="clearTimeout(myVar)">停止执行</button>
<script>
function myFunction() {    alert('Hello'); }
</script>

window.setInterval(function, milliseconds);
window.clearInterval(timerVariable);

var myVar = setInterval(myTimer, 1000);
function myTimer() {
    var d = new Date();
    document.getElementById("demo").innerHTML = d.toLocaleTimeString();
}
<button onclick="clearInterval(myVar)">停止时间</button>
```
