## python教程

### python简介
> 读史明智，鉴往知来。

Python是一种计算机程序设计语言。是一种动态的、面向对象的脚本语言，最初被设计用于编写自动化脚本(shell)，随着版本的不断更新和语言新功能的添加，越来越多被用于独立的、大型项目的开发。
Python的设计哲学是“优雅”、“明确”、“简单”。
Python是完全面向对象的语言。
Python是著名的“龟叔”Guido van Rossum在1989年圣诞节期间，为了打发无聊的圣诞节而编写的一个编程语言。
第一个缺点就是运行速度慢。第二个缺点就是代码不能加密。
声明：本笔记内容来自互联网，借鉴了[廖雪峰](https://www.liaoxuefeng.com/)的教程，在此感谢。

### 基础
Python 是一种计算机编程语言。需要编译器或者解释器把符合语法的程序代码转换成 CPU 能够执行的机器码。
python 语法主要靠缩进，一般使用 4 个空格进行缩进。
以 # 开头的语句是注释，python 是区分大小写的。

#### 数据类型和变量
**整数**

在程序中的表示方法和数学上的写法一模一样，例如：1，100，-8080，0，等等。
十六进制用0x前缀和0-9，a-f表示，例如：0xff00，0xa5b4c3d2，等等。
Python3 支持 int、float、bool、complex（复数）。
在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
内置的 type() 函数可以用来查询变量所指的对象类型。type() 不会认为子类是一种父类类型； isinstance() 会认为子类是一种父类类型。
在 Python2 中是没有布尔型的，它用数字 0 表示 False，用 1 表示 True。到 Python3 中，把 True 和 False 定义成关键字了，但它们的值还是 1 和 0，它们可以和数字相加。

**浮点数**

浮点数也就是小数，之所以称为浮点数，比如 1.23x10^9 、12.3x10^8。浮点数可以用数学写法，如1.23，3.14，-9.01，等等。也可以用科学计数法表示，把10用 e 替代，1.23x10^9就是1.23e9，或者12.3e8，0.000012可以写成1.2e-5，等等。

整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的（除法难道也是精确的？是的！），而浮点数运算则可能会有四舍五入的误差。

**字符串**

Python中的字符串用单引号 ' 或双引号 " 括起来，同时使用反斜杠 \ 转义特殊字符。
索引值以 0 为开始值，-1 为从末尾的开始位置。
加号 + 是字符串的连接符， 星号 * 表示复制当前字符串，紧跟的数字为复制的次数。
Python 使用反斜杠(\)转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 r，表示原始字符串。如 \n 表示换行，\t 表示制表符等等。

**布尔值**

布尔值和布尔代数的表示完全一致，一个布尔值只有True、False两种值，要么是True，要么是False，在Python中，可以直接用True、False表示布尔值。
布尔值可以用 and、or 和 not 运算。

**空值**

空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。

**变量**

变量在程序中就是用一个变量名表示了，变量名必须是大小写英文、数字和_的组合，且不能用数字开头。比如 a = 1、t_007 = 'T007'、Answer = True 等等。
这种变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。int a = 123;  此为静态语言。
a = 'ABC' ，Python解释器干了两件事情：
	1. 在内存中创建了一个'ABC'的字符串；
	2. 在内存中创建了一个名为a的变量，并把它指向'ABC'。
	3. 也可以把一个变量a赋值给另一个变量b，这个操作实际上是把变量b指向变量a所指向的数据。

**常量**

常量就是不能变的变量，比如常用的数学常数π就是一个常量。在Python中，通常用全部大写的变量名表示常量：PI = 3.14159265359。
在Python中，有两种除法：
一种除法是 /：10 / 3  >>> 3.3333333333333335
另一种除法是 //，称为地板除：10 // 3 >>> 3
余数运算，可以得到两个整数相除的余数：10 % 3 >>> 1

#### 字符串和编码

**编码**

ASCII 编码：127个字符，大小写英文字母、数字和一些符号。
GB2312 编码：ASCII 不能处理中文，就发展了 GB2312 编码。
Unicode 编码：统一了编码问题。常用两个字节表示一个字符，特殊的需要4个字节。
UTF-8 编码：由于 Unicode 编码在存储全英文时会多占用空间，发展出了可变长的 UTF-8 编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。
字符 A 在 ASCII 码中用 01000001 表示，即65，用 Unicode 表示是 00000000 01000001 ，用 UTF-8 表示 01000001 。

在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。
用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件。
浏览网页的时候，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器。

**字符串**

对于单个字符的编码，Python 提供了 ord() 函数获取字符的整数表示，chr() 函数把编码转换为对应的字符。 ord('A') >>> 65 ，chr(66) >>> ‘B’ 。
如果知道字符的整数编码，还可以用十六进制这么写 str，'中文' >>> '\u4e2d\u6587' 

由于 Python 的字符串类型是 str，在内存中以 Unicode 表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把 str 变为以字节为单位的 bytes 。
对 bytes 类型的数据用带b前缀的单引号或双引号表示 ：x = b'ABC' 。bytes 的每个字符都只占用一个字节。'ABC'.encode('ascii') >>> b'ABC' ，'中文'.encode('utf-8') >>> b'\xe4\xb8\xad\xe6\x96\x87' 。

从网络或磁盘上读取了字节流，那么读到的数据就是 bytes。要把 bytes 变为s tr，就需要用 decode() 方法：b'ABC'.decode('ascii') >>> 'ABC' ，b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8') >>> '中文' 。

计算 str 包含多少个字符，可以用 len() 函数：len('中文') >>> 2，len('ABC') >>> 3。
如果换成bytes，len()函数就计算字节数：len(b'\xe4\xb8\xad\xe6\x96\x87') >>> 6。
```python
#!/usr/bin/env python3    --- 告诉Linux/OS X系统，这是个可执行程序
# -*- coding: utf-8 -*-   --- 告诉Python解释器，按照UTF-8编码读取源代码
# 申明了UTF-8编码，还需要确保文本编辑器正在使用UTF-8 without BOM编码
```

**格式化**
在 Python 中，采用的格式化方式和 C 语言是一致的，用 % 实现。字符串中单纯想输出 % 符号，需要转义，即 %%。

|  占位符   |   替换内容  |
| --- | --- |
|  %d   |   整数，'%2d-%03d' % (3, 1) >>> 前面两个空格，后面001  |
|  %f   |  浮点数，‘%.2f’ % 3.141592653 >>> 3.14   |
|  %s   |   字符串  |
|  %x   |  十六进制整数   |

format()
另一种格式化字符串的方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……。'hello {0}, I\'am {1}'.format('Lucy','Keith') >>> "hello Lucy, I'am Keith"

#### 列表和元组

**列表 list**

list 是另一种数据类型。list 是一种有序的集合，可以随时添加或删除元素。
```python
list1 = ['Michael', 'Tom', 'Jerry']
print(list1) >>> ['Michael', 'Tom', 'Jerry']
list1.append("keith")
print(list1) >>> ['Michael', 'Tom', 'Jerry', 'keith']
list1.insert(1, "Lucy")
print(list1) >>> ['Michael', 'Lucy', 'Tom', 'Jerry', 'keith']
list1.pop()
print(list1) >>> ['Michael', 'Lucy', 'Tom', 'Jerry']
list1.pop(1)
print(list1) >>> ['Michael', 'Tom', 'Jerry']
list1[1] = "dollars"
print(list1) >>> ['Michael', 'dollars', 'Jerry']
```

**元组 tuple**

另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改。tuple 定义一个元素的时候为了产生歧义，需要在元素后面添加一个逗号，比如 myTuple = (1, ) ，不加逗号认为是一个运算，即 myTuple = 1。
```python
tuple1 = (32, 23, ['a', 'b'], 'z')
print(tuple1) >>> (32, 23, ['a', 'b'], 'z')
tuple1[2][0] = 'X'
print(tuple1) >>> (32, 23, ['X', 'b'], 'z')
```
这并不是元组发生了变化，而是元组中的列表 list 发生了变化，改变了列表中的指向，元组中的指向是没有发生变化的。

#### 条件判断

为了进行流程控制，根据不同的条件进行不同的操作，就有了分支语句。
条件判断语句是使用 if 来实现的。

```python
age = int(input("请输入您的年龄："))
if age >= 18:
    print("可以上网了")
elif age >= 12:
    print("还差得远呢")
else:
    print("回家呆着去")
```

#### 循环

第一种循环 for... in... 循环：
```python
names = ['Michael', 'Tom', 'Jerry']
for name in names:
    print(name)
>>> 'Michael'
>>> 'Tom'
>>> 'Jerry'

sum = 0
for x in range(101):
    sum += x
print(sum) >>> 5050
```
第二种循环 while 循环：
```python
num = 5
while num > 0:
    print(num) >>> 5 4 3 2 1
    num -= 1 
```
break 和 continue ：
在循环中，break语句可以提前退出循环。
在循环过程中，也可以通过continue语句，跳过当前的这次循环，直接开始下一次循环。

#### 字典和集合

**字典 dict**

Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
与 list 比较，dict 随着数据的增加，读取时间不会增加，但是浪费内存多，是采用空间换时间的一种方法。
dict的key必须是不可变对象。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key。
```python
d = {'Michael': 95, 'Tom': 85, 'Jerry':70}
d['Jack'] = 85
print('Jack' in d) >>> True
print(d.get("Lucy", -1)) >>> -1
print(d) >>> {'Michael': 95, 'Tom': 85, 'Jerry': 70, 'Jack': 85}
d.pop('Jerry')
print(d) >>> {'Michael': 95, 'Tom': 85, 'Jack': 85}
```

**集合 set**

set 和 dict 类似，也是一组 key 的集合，但不存储 value。由于 key 不能重复，所以，在 set 中，没有重复的 key。
set 是一种无序的集合。
```python
s = set([2, 4, 3])
s1 = set([3, 2, 8])
print(s) >>> {2, 3, 4}
s.add(6)
print(s) >>> {2, 3, 4, 6}
s.remove(3)
print(s) >>> {2, 4, 6}
print(s & s1) >>> {2}
print(s | s1) >>> {2, 3, 4, 6, 8}
```

### 函数

为了简化重复操作，就把重复操作放进一个函数中，使用时只需要调用就可以了，函数的调用是通过函数名进行调用的。
python 内置了许多内置的函数：
```python
a = abs(123)
b = abs(-123)
c = abs(-1.01)
print(a, b, c) >>> 123 123 1.01 计算绝对值

a = max(1, 3, 5, 7)
b = max(3, -8, 6, 9)
print(a, b) >>> 7 9 计算最大值

n1 = 255
n2 = 1000
print(hex(n1), "---", hex(n2))
```

#### 定义函数

在Python中，定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。
```python
def my_abs(x):
    if x > 0:
        return x
    else:
        return -x

print(my_abs(-12.3)) >>> 12.3
print(my_abs(12.3)) >>> 12.3
print(isinstance(123, (int, float))) >>> True

import math

def quadratic(a, b, c):
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)) or not isinstance(c, (int, float)):
        raise TypeError('bad operand type')
    if a == 0:
        return 0
    if (b * b - 4 * a * c) < 0:
        return -1
    num1 = (- b + math.sqrt((b * b - 4 * a * c))) / (2 * a)
    num2 = (- b - math.sqrt((b * b - 4 * a * c))) / (2 * a)
    return num1, num2
	
print(quadratic(2, -5, -12)) >>> (4.0, -1.5)
print(quadratic(2, 3, 'c')) >>> TypeError: bad operand type
```

#### 参数函数

**默认参数**

当函数有多个参数时，把变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。
```python
def person(name, age, sex="female"):
    print("My name is :", name)
    print("I'm", age, "years old")
    print("I'am a", sex)

person("Keith", 25)
```
如果默认参数是指向可变对象，会引起改变，再次调用时原来调用的值还在。** 定义默认参数要牢记一点：默认参数必须指向不变对象！**
```python
def L(l=[]):
    l.append("end")
    return l

print(L([1, 2, 3]))  # [1, 2, 3, 'end']
print(L())  # ['end']
print(L())  # ['end', 'end']

# 可以用 None 这个不可变对象来设置
def M(m=None):
    if m is None:
        m = []
    m.append("end")
    return m
```

**可变参数**

定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个```*```号。调用该函数时，可以传入任意个参数，包括0个参数。
```python
def sum(*num):
    sums = 0
    for x in num:
        sums += x
    return sums


print(sum(1, 2, 3))  # 6
```

**关键字参数**

可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。
```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)


extra = {'city': 'Beijing', 'job': 'Engineer'}
print(person('Jack', 24, city=extra['city'], job=extra['job']))

person('Jack', 24, **extra) # 上面的写法和这个写法一样，相当于传入地址，但实际只是拷贝了一份

# 在传递参数时，city='city' 昨天不能加引号，可以理解为传入一个值，系统实现变成字典
```

**命名关键字参数**

对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。
如果要限制关键字参数的名字，就可以用命名关键字参数。
```python
# 方法一： 在参数之间添加一个```*```分隔符，
def person(name, age, *, city, job):
    print(name, age, city, job)

person("zhangsan", 56, city="changsha", job="IT")

# 方法二： 把 * 换成 *args
def person(name, age, *ags, city, job):
    print(name, age, city, job)
```

**参数组合**

在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
```python
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
```

```*args``` 是可变参数，args 接收的是一个 tuple；
```**kw``` 是关键字参数，kw 接收的是一个 dict。

#### 递归函数

在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。
```python
# 计算 n 的阶乘
def fact(n):
    if n == 1:
        return 1
    return n * fact(n-1)
```
使用递归函数需要注意防止栈溢出。解决递归调用栈溢出的方法是通过尾递归优化，尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。
```python
def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
	
# 汉诺塔
def move(n, a, b, c):
    if n == 1:
        print(a, "-->", c)
    else:
        move(n - 1, a, c, b)
        move(1, a, b, c)
        # print(a, "-->", c)
        move(n - 1, b, a, c)
```

### 特性

在Python中，代码不是越多越好，而是越少越好。代码不是越复杂越好，而是越简单越好。
```python
# 构造一个1, 3, 5, 7, ..., 99的列表
L = []
n = 1
while n <= 99:
    L.append(n)
    n = n + 2
```

#### 切片

取一个list或tuple的部分元素。
```python
# 使用切片操作，实现一个 trim 函数
def trim(s):
    while s[:1] == ' ':
        s = s[1:]
    while s[-1:] == ' ':
        s = s[:-2]
    return s
```

#### 迭代

如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。
在Python中，迭代是通过for ... in来完成的，而很多语言比如C语言，迭代list是通过下标完成的。
Python的for循环不仅可以用在list或tuple上，还可以作用在其他可迭代对象上。只要是可迭代对象，无论有无下标，都可以迭代，比如dict就可以迭代：
```python
my_dict = {"k1":1,"k2":2,"k3":3}
for key in my_dict:
    print(key)
```
默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()。

判断一个对象是不是可迭代对象：通过 collections 模块的 Iterable 类型判断。
```python
from collections import Iterable
print(isinstance("ABC", Iterable))
print(isinstance([1, 2, 3], Iterable))
print(isinstance(123, Iterable))  # false
print(isinstance({'k': 'v'}, Iterable))

# 迭代得到最大值最小值
def findMinAndMax(L):
    if not L:
        return (None, None)
    mx = mn = L[0]
    for v in L:
        if mx < v:
            mx = v
        if mn > v:
            mn = v
    return (mn, mx)
```

#### 列表生成式

列表生成式即 List Comprehensions，是 Python 内置的非常简单却强大的可以用来创建 list 的生成式。
```python
# 生成 [1,2,3,4,5,6,7,8,9,10]
print(list(range(1, 11)))

# 生成 [1x1, 2x2, 3x3, ..., 10x10]
L = []
for x in range(1, 11):
    L.append(x * x)
print(L)   # 传统做法

print([x*x for x in range(1,11)]) # 列表生成式

# [4, 16, 36, 64, 100]
print([x * x for x in range(1, 11) if x % 2 == 0])
# ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
print([m + n for m in 'ABC' for n in 'XYZ'])

import os
print([x for x in os.listdir('.')]) # 生成当前文件名的列表

d = {'x': 'A', 'y': 'B', 'z': 'C'}
print([k + '=' + 'v' for k, v in d.items()])
```
列表生成式之中必须要有中括号 ```[ ]```。

#### 生成器

通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。
python 中通过某种算法推算出后续元素的机制，成为生成器： generator 。

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的```[]```改成```()```，就创建了一个generator：
```python
print([x for x in range(1, 11)]) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print((x for x in range(1, 11))) # <generator object <genexpr> at 0x04EED420>
```
获取打印 generator 中的每一个元素使用 next() 函数。
```python
L2 = (x for x in range(1, 11))
print(next(L2)) # 1
print(next(L2)) # 2
print(next(L2)) # 3

for n in L2:
    print(n) # generator 时一个迭代器
```
斐波那契数列表示：
```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        print(b)
        a, b = b, a + b # 相当于 t = (b, a + b) a = t[0] b = t[1]
        n = n + 1
    return 'done'
```
把```fib```函数变成```generator```，只需要把```print(b)```改为```yield b```就可以了。如果一个函数定义中包含 yield 关键字，那么这个函数就不再是一个普通函数，而是一个 generator ：
```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```
函数时遇到 return 就返回。而 generator 在每次调用 next() ，遇到 yield 语句返回，再次执行时从上次返回的 yield 语句处继续执行。
调用 generator 时，首先要生成一个 generator 对象，然后用 next() 函数不断获得下一个返回值：
```python
f = fib(6)
print(f) # <generator object fib1 at 0x051CD420>
print(next(f))
```
用 for 循环调用 generator 时，发现拿不到 generator 的 return 语句的返回值。如果想要拿到返回值，必须捕获 StopIteration 错误，返回值包含在 StopIteration 的 value 中：
```python
f2 = fib1(6)
while True:
    try:
        x = next(f2)
        print('x:',x)
    except StopIteration as e:
        print('Generator return value:',e.value)
        break
```
杨辉三角的实现：
```python
def triangles():
    L = [1]
    ret = [1]
    while True:
        yield L
        # L = [sum(i) for i in zip([0] + L, L + [0])]
        # L = [1] + [L[i] + L[i + 1] for i in range(len(L) - 1)] + [1]
        L = [1] + [L[i - 1] + L[i] for i in range(1, len(L))] + [1]
# 每一行的个数等于行数，除了左右两边的数为1，中间的数等于上一行两个数相加
```

#### 迭代器

直接作用于 for 循环的数据类型有以下几种：
一类是集合数据类型，如 list 、tuple 、dict 、set 、str 等；
一类是 generator ，包括生成器和带 yield 的 generator function 。

可以直接作用于 for 循环的对象统称为```可迭代对象```：```Iterable``` 。
可以使用 isinstance() 判断一个对象是否是 Iterable 对象：
```python
from collections import Iterable
print(isinstance([], Iterable)) # True
print(isinstance((), Iterable)) # True
print(isinstance({}, Iterable)) # True
print(isinstance(set([]), Iterable)) # True
print(isinstance('ABC', Iterable)) # True
```
生成器不但可以作用于 for 循环，还可以被 next() 函数不断调用并返回下一个值，直到最后抛出 StopIteration 错误表示无法继续返回下一个值了。
可以被 next() 函数调用并不断返回下一个值的对象称为```迭代器```：```Iterator```。
生成器都是 Iterator 对象，但 list、dict、str 虽然是 Iterable，却不是 Iterator。
把 list、dict、str 等 Iterable 变成 Iterator 可以使用```iter()```函数。

### 函数式编程

函数是 Python 内建支持的一种封装，我们通过把大段代码拆成函数，通过一层一层的函数调用，就可以把复杂任务分解成简单的任务，这种分解可以称之为面向过程的程序设计。函数就是面向过程的程序设计的基本单元。

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

函数式编程的一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！

#### 高阶函数

**变量可以指向函数**：函数本身也可以赋值给变量，即：变量可以指向函数。``` f = fucName ```
**函数名也是变量**：函数名其实就是指向函数的变量。
**传入函数**：函数作为参数传入函数，这种函数就称之为高阶函数。
```python
def add(x, y, f):
    return f(x) + f(y)
```
**map / reduce**：
map() 函数接收两个参数，一个是函数，一个是 Iterable，map 将传入的函数依次作用到序列的每个元素，并把结果作为新的 Iterator 返回。
结果是一个 Iterator，Iterator 是惰性序列，因此通过 list() 函数让它把整个序列都计算出来并返回一个 list。
```list(map(str, [1, 2, 3])) >>> ['1', '2', '3']```
reduce把一个函数作用在一个序列 [x1, x2, x3, ...] 上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算。
```python
from functools import reduce
def fn(x, y):
    return x * 10 + y
print(reduce(fn, [1, 3, 5, 7, 9])) # 13579

DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
def char2num(s):
    return DIGITS[s]
def str2int(s):
    return reduce(lambda x, y: x * 10 + y, map(char2num, s))
# 把字符串转为数字，并且返回 reduce 作用后的值

# 把字符串'123.456'转换成浮点数123.456
def str2float(s):
    l = len(s.split('.', 1)[1])
    s = ''.join(s.split('.', 1))
    def f2(x, y):
        return x * 10 + y
    def char2num(s):
        return DIGITS[s]
    return (reduce(f2, map(char2num, s))) / (10 ** l)
```