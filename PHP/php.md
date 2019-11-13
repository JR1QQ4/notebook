# php

1.变量

```
$num = 1234;  // 大小写敏感
echo "字符串拼接".$num; 
echo '单引号中使用变量：$num'  // $num会被当成字符串，直接输出
echo "双引号中使用变量：$num"  // $num会变成变量

$arr = array("hello","world");
print_r($arr);  // Array ([0] => hello [1] => world)
echo $arr[1];
$arr1 = array("username"=>"zhangsan","age"=>12);
print_r($arr1);  // Array ([username] => zhangsan [age] => 12)
$arr2 = array();  // 二维数组
$arr2["a"] = array("1"=>"123","2"=>"234");
$arr2["b"] = array("3"=>"345","4"=>"456");
$arr2["c"] = array("5"=>"567","6"=>"678");

echo：输出简单数据类型，如字符串、数值，直接输出$arr会报错，可以输出$arr[0]
print_r()：输出复杂数据类型，如数组
var_dump()：输出详细信息，如对象、数组，详细信息会有长度这些
```

2.函数

```
json_encode($arr)  // 转换成json字符串，会转码
function Foo($info){  // 函数名不区分大小写，foo==Foo；有提升
    return $info*10;  
}

http协议常用请求方式（增删改查）：
get     用来从服务器获取数据
post    添加数据
put     修改数据
delete  删除数据

$get = $_GET["key"]  // 得到url地址中传递的参数的值，?key=123

<form method="post" action="my.php">...</form>
header("Content-Type:text/plain;charset=utf-8");  // 设置服务器响应格式MIME和编码
header("Content-Type:text/xml;");  // 设置成xml解析
$username = $_GET["username"];
$pw = $_GET["password"];

sleep(3);  // 等待3秒
```


