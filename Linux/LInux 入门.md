## Linux 入门
1.Linux 前身 Unix。
* 1968年，Multics 项目。MIT、Bell 实验室、美国通用电气有限公司一起开发 Multics 项目，后期开发进度不是很好，MIT和Bell实验室离开了项目的开发，最终项目搁浅。
* 1970年，Unix 诞生。在 Multics 项目时，一个开发成员开发了一款游戏（trabel space 遨游太空），因为两个实验室离开，导致这名开发人员没发玩游戏。后来他提议组织人员重新开始该项目，也就出现了1970年的Unix。当时的Unix操作系统是使用汇编语言开发的。时间戳 150000000 1970-1-1 00:00:00
* 1973年，用 C 语言重写 Unix。
* 1975 年，Bell 实验室允许大学使用 Unix。
* 1975 年，Bell 实验室允许大学使用 Unix 操作系统用于教学作用，而不允许用于商业用途。

2.Linux 诞生
Linus，李纳斯·托瓦兹，当时是荷兰在校大学生。1991年 0.0.1版本，使用Unix操作系统，然后对其系统的底层进行修改，放到学校的网站上，原先命名 Linus's Unix，后觉得名字不好改名 Linux。1992年0.0.2版本，1994年1.0版本，2003年2.6版本，版本是内核版本，不是分支版本。
操作系统其实就是核心与其提供的接口工具，核心就是 Kernel。Kernel 为了达成使用者所需要的正确运算结果，必须要管理的事项有：系统呼叫接口；行程管理；内存管理；档案系统管理；装置的驱动。

3.开源
斯特曼 Stallman，开源文化倡导人，1983年 GNU计划，1985年 FSF基金会，1990年 Emacs、GCC（c语言的编译器）、程序库，1991年 他找 Linus 商谈 Linux 开源，1992年 GNU/Linux。

4.Linux 系统特点：开放性、多用户、多任务、稳定性
5.Linux 分支：著名的有 ubuntu、debian、centos、redhat、suse等

6.Linux 安装：真机安装；虚拟机安装。虚拟机，模拟真实的电脑环境，比较有名的虚拟机，vmware和virtual box(轻量级)。[vmware下载](https://www.vmware.com/)  [virtual box下载](https://www.virtualbox.org/)

7.Linux 文件：Linux 一切皆文件。

### Linux 指令
在 Linux 终端（命令行）中输入的就是指令，指令的通用格式：#指令主体 [选项] [操作对象]。一个指令包含多个选项，操作对象也可以是多个。以下部分只统计了部分常用指令。

#### 基础指令

1.ls
* #ls ：查看当前工作目录下的所有文件/文件夹
	* #ls 路径名，查看指定目录下文件/文件夹，#ls ../../root
* #ls -lha [路径]，-l 表示以详细列表显示，-a显示隐藏文件，-h以可读性更高的方式显示

2.pwd ， #pwd ，打印当前工作路径

3.cd ， #cd 路径，切换当前工作目录，cd ~ 切换到家目录

4.mkdir 
* #mkdir 路径，创建目录，这个目录可以是文件夹名称
* #mkdir -p 路径，一次性创建多层文件夹
* #mkdir 路径1 路径2...

5.touch
* #touch 路径，路径可以是文件名
* #touch 路径1 路径2，创建多个文件

6.cp
* #cp 被复制的文档路径 被复制到的路径，cp a.txt /home/c/a.txt
	* cp a.txt /home/c/a1.txt ，复制过程中并重命名
* #cp -r 被复制路径 目的地，-r表示递归复制

7.mv
* #mv 需要移动的文档路径 需保存的路径，移动后原始文件不在原来位置
	* 重命名可以用移动使用

8.rm
* #rm 选项 需要移除的文档路径
	* -f ：强制删除，不会有提示
	* -r ：递归删除
* #rm -rf 文档路径1 文档路径2...，批量删除多个
	* #rm -rf linux*，删除以linux开头的文档，*表示通配符

9.vim
* #vim 文件路径，文本编辑

10.输出重定向，#正常执行的指令 {>|>>} 文件路径，文件不存在就创建
* > ：覆盖输出，会覆盖原先的文件内容
* >> ：追加输出，不会覆盖原始文件内容，在原始内容末尾添加

11.cat
* #cat  文件的路径，直接打开文件，类似vim
* #cat 文件路径1 文件路径2... > 文件路径，合并文件名到文件路径

12.clear | ctrl +L，#clear | Ctrl + L，清屏

#### 文档类指令

1.df
* #df -h ：以可读性更高的方式查看磁盘空间

2.free
* #free -m ：查看内存的使用情况，-m表示兆M，-g表示G

3.head
* #head -n 文件路径，查看文件的前n行，n是数字

4.tail
* #tail -n 文件路径，查看文件的后n行，n表示数字
* #tail -f 文件路径，查看文件的动态变化，变化的内容不是用户手动添加的
	* #tail -f text.txt，ls -lh > text.txt，一般用于查看系统的日志

5.less
* #less 文件路径，以较少的内容进行输出，查看文件，可以使用辅助键查看
	* 数字+回车、空格键，按q退出

6.wc
* #wc -lwc 文件路径，统计文件内容信息（包含行数、单词数、字节数）
	* -l ：表示行数，-w ：表示单词数，-c ：表示字节数

7.date
* #date ，查看、设置时间日期，CST当地时间
	* #date +%F ，等价于 #date "%Y-%m-%d" ，输出形式2019-05-12
	* #date +"%F %T" ，等价于 #date +"%Y-%m-%d %H:%M:%S" 引号让年月日和时分秒成为一个整体，2019-05-12 16:01:00
	* #date -d "-1 day age" +"%Y-%m-%d %H:%M:%S"，获取之前或之后的日期时间，-1之前，+1之后，day天，month月，year年

8.cal
* #cal ，等价于 #cal -1 ，直接输出当前月份的日历，
	* #cal -3，输出本月上月下月日历，
	* #cal -y 年份，输出某一年份的日历

9.管道 `|`，不能单独使用
* 过滤，如 #ls / | grep y，查询根目录下包含y的文档
* 扩展处理，统计某个目录下的文档的总个数，比如 #ls / | wc -l

#### 其他指令

1.hostname，读取、设置主机名，设置的主机名是临时的
* #hostname，输出完整主机名localhost.hostname 
	* #hostname -f，输出主机名中的FQDN全限定主域名localhost

2.id，查看一个用户的一些基本信息
* #id ，uid用户id，gid组id，组表示附加组
	* #id 用户名，显示指定用户的基本信息
* 验证用户信息通过文件 /etc/passwd ，验证用户组信息 /etc/group

3.whoami ，显示当前登录的用户名
* #whoami ，一般用于 shell 脚本，获取当前操作的用户名方便记录日志

4.ps ，查看服务器的进程信息
* #ps -ef ，UID用户id，PID进程id，PPID父级进程id，C表示CPU占用率，STIME启动时间，TTY终端设备（?表示不是终端发起），TIME进程执行时间，CMD进程名称或路径
	* -e ，等价于 -A，表示列出全部的进程
	* -f ，显示全部的列（显示全字段）
	* #ps -ef | grep 进程名称，查看指定进程

5.top ，查看服务器的进程占的资源
* #top ，动态显示进程占用资源，按q退出，
	* PR权重，VIRT虚拟内存，RES常驻内存，SHR共享内存，S进行状态S表示睡眠R表示运行，TIME执行的呃时间，COMMAND进程名称或路径

6.du ，查看目录的真实大小
* #du -sh 目录路径，目录里面的文档大小
	* -s ，显示汇总的大小；-h 以高可读性的形式进行显示

7.find ，用于查看文件
* #find 路径范围 选项 选项的值，
	* -name，按照文档名称搜索（支持模糊搜索）
	* -type，按文档的类型进行搜索，文档类型：-表示文件find中用f表示，d表示文件夹
		*  比如 #find /etc -name *.conf | wc -l ，#find /etc -type f | wc -l

8.service ，用于控制一些软件的服务启动、停止、重启
* #service 服务名 start|stop|restart ，比如#service httpd start ，启动之后可以使用 #ps -ef | grep httpd 查看进程

9.kill ，关闭进程或者服务
* #kill 进程PID ，如果没有对应的PID会有相应提示
* #killall 进程名称 ，不需要使用ps查看PID，#killall httpd

10.ifconfig ，操作网卡
* #ifconfig ，获取网卡信息，ipv4地址是在inet addr后面

11.reboot ，重启计算机
* #reboot ，重启；#reboot -w ，模拟重启但不重启，只写关机和开机的日志

12.shutdown ，关机
* #shutdown -h now ["关机提示"]或 #shutdown -h 15:25 ["关机提示"]，立即关机和定时关机
	* Ctrl + c ，或者 #shutdown -c ，(centos7.X之后)取消关机计划
* #init 0 ，#hait ，#poweroff ，其他关机方式

13.uptime ，输出计算机的持续在线时间，开机到现在运行的时间
* #uptime ，其中15：58表示15小时，users连接数，load average负载,windows中可以使用systeminfo

14.uname ，获取计算机操作系统相关信息
* #uname ，获取操作系统的类型
	* #uname -a ，操作系统完整信息，内核版本，发布时间 

15.netstat ，查看网络连接状态
* #netstat -tnlp ，查看网络连接状态
	* -t 列出tcp协议的连接，
	* -n 将地址从字母转为ip地址，将协议转换为端口号来显示
	* -l 过滤出“stat（状态）”列出其值为LISTEN（监听）的连接
	* -p 显示发起连接的进程pid和进程名称

16.man ，manual 手册
* #man 指令 ，查看指令的信息，按q退出

17.其他一些
* 删除光标前或后的内容，ctrl+u删除前面的，ctrl+k删除后面的
* 删除/tmp下所有A开头的文件，#rm -f /tmp/A*
* 把/etc/passwd备份到/tmp目录下，#cp /etc/passwd /tmp/
* 查看最后创建的3个用户，#tail -3 /etc/passwd
* 统计当前系统总的用户数，#wc -l /etc/passwd ，或 #cat /etc/passwd | wc -l
* 创建/tmp/test.conf文件，#touch /tmp/test.conf
* 用vim打开/tmp/test.conf，#vim /tmp/test.conf
* 查看/etc/passwd的头3行和尾3行，#head -3 /etc/passwd ，#tail -3 /etc/passwd
* 一次性创建目录/test/1/2/3/4，#mkdir -p /test/1/2/3/4
* 返回当前账户家目录，#cd ，#cd ~
* 查看/etc所占磁盘空间，#du -sh /etc
* 删除/tmp下所有文件，#rm -rf /tmp/*
* 启动Apache服务，并检查是否启动成功，#service httpd start ，#ps -ef | grep httpd
* 杀死Apache的进程，#killall httpd ，#kill apache进程PID

### vim 编辑器
vi 编辑器是系统自带的编辑器，类似windows系统中的记事本。vim编辑器是vi的升级版。

![vim 编辑器](./images/vi.gif)

vim有三种模式：
* 命令模式：打开文件后默认进入的模式，不能直接对文件编辑，可以输入快捷键进行一些操作（删除行，复制行，移动光标，粘贴等等）。
* 编辑模式（输入模式）：对文件的内容进行编辑。
* 末行模式（尾行模式）：可以在末行输入命令来对文件进行操作（搜索、替换、保存、退出、撤销、高亮等等）。

vim打开文件的方式：
* #vim 文件路径，打开指定的文件
* #vim +数字 文件的路径，打开指定的文件，并且光标移动到指定行
* #vim +/关键词 文件的路径，打开指定的文件，并且高亮显示关键词
* #vim 文件路径1 文件路径2 ...，同时打开多个文件

模式切换：

![vim模式切换](./images/vim-vi-workmodel.png)



#### 命令模式
1.光标移动
* 光标移动到行首：shift + 6 或 ^
* 光标移动到行尾：shfit + 4 或 $
* 光标移动到首行：gg
* 光标移动到末行：G 或 shift + g
* 翻屛：向上ctrl+b ，向下ctrl+f
* 光标快速移动：
	* 移动到指定的行：数字G，10G移动到10行
	* 向上/向下移动n行：向上数字+↑，向下数字+↓
	* 向左/向右移动n个字符：向左数字+←，向右数字+→
2.复制
* 复制光标所在行：yy
	* 粘贴：p
* 复制光标及以下行：数字yy，3yy表示复制3行
* 可视化复制：ctrl+v ，然后选择复制区域，并按下 yy 复制

3、剪切/删除
* 剪切/删除光标所在行：dd ，剪切了不粘贴就是删除
* 剪切/删除当前行及下行：数字dd，3dd剪切3行
* 剪切/删除当前行，删除行光标不上移动：D 或 shift d

4.撤销/恢复
* 撤销上一步：u 或者 :u
* 恢复：ctrl + r ，取消之前的撤销

#### 末行模式
末行模式由命令模式进入，按 “:” 或者 “/” 进入，“/”表示查找。

1.保存和退出
* 保存文件：":w" 
	* 另存文件：“:w 路径”，:w 2.txt 另存为2.txt，源文件保存
* 退出文件：“:q”
* 保存并退出：“:wq”

2.强制
* 强制退出：“:q!” ，之前修改的操作不保存
* 调用外部命令，文件暂时隐藏：":! 指令"，:! ls -lah，查看文档

3.搜索和替换
* 搜索查找：“/关键词”，/login 搜索login，前面没有“:”。
	* 在搜索结果中向上/向下查看结果：上N ，下n
	* 取消高亮：“:nohl”，查找之后会一直高亮，取消之后才会没有
* 替换搜索到的内容：
	* “:s/要搜索的关键词/新的内容” ，只替换光标所在行第一处符合条件的内容
	* “:s/要搜索的关键词/新的内容/g” ，替换光标所在行的内容
	* “:%s/要搜索的关键词/新的内容” ，替换整个文档中每行中第一处符合条件的内容
	* “:%s/要搜索的关键词/新的内容/g” ，替换所有匹配到的内容
		* %表示整个文档，g 表示全局

4.其他
* 显示行号：“set nu”，取消行号：“set nonu”，设置的只是暂时的
* 同时打开多个文件：vim 文件名1 文件名2 文件名3 ...
	* 查看当前打开的文件名：":files"
		* %a表示当前活跃（active）的文件，#表示上一个打开的文件
	* 切换文件：
		* 指定文件名称：“:open 文件名称”
		* 切换上一个/下一个文件：下一个":bn"，上一个":bp"

#### 编辑模式
在命令模式下输入i、a、o、I、A、O、S等进入编辑模式。
* i ：在光标所在字符前插入
* a ：在光标所在字符后插入
* o ：在光标所在行的下面另起一新行插入
* I ：在光标所在行的行首开始插入，如果行首有空格则在空格之后插入
* A ：在光标所在行的行尾开始插入
* O ：在光标所在行的上面另起一行开始插入
* S ：删除光标所在行并开始插入

#### 其他
1.代码着色：控制代码的颜色。
* 开启和关闭代码着色：“:syntax on”开启，“:syntax off”关闭

2.vim中的计算器的使用
* 按下按键“ctrl + r”，会出现引号"，然后输入等到“=”，光标跳到最后一行，输入要计算的算数

3.vim 的配置，一般包含三种情况
1. 在文件打开的时候在末行模式下输入的配置是临时的；
2. 个人配置文件（~/.vimrc），如果没有则可新建
3. 全局配置文件（vim自带的，/etc/vimrc），配置冲突时以个人配置为准
	* 在.vimrc中设置，比如显示行号set nu	，比如着色syntax on

4.异常退出
* 在编辑文件之后并没有正常退出wq，而是遇到突然关闭终端或断电的情况，就会出现异常退出。
	* 把出现的交换文件（在编辑过程中产生的临时文件，'.文件名.swp'）删除掉

5.别名机制
* 相当于创建属于自己的自定义命令，别名机制依靠一个别名映射文件"~/.bashrc"。
	* 使用vim打开文件，添加别名比如alias cls='clear'，添加之后需要重新登录

6.退出方式
* vim除了“:q”或者":wq"退出登录，还可以使用“:x”保存退出
	* 使用 wq 退出时会修改时间，使用 :x 退出时不会修改时间，编译会修改时间
	* 大写的 :X 是对文件进行加密

### linux 自由服务
自由服务，即不需要用户独立去安装的软件的服务，而是当系统安装好之后就可以直接使用的服务（内置的）。

#### 运行模式

运行模式也称为运行级别。
在 linux 中存在一个进程：init ，进程id是 1。查看 #ps -ef | grep init
该进程存在一个对应的配置文件：inittab （系统运行级别配置文件，位置 /etc/inittab）。在 Centos6.5 中存在 7 种运行级别。
id: 5: initdefault:
* 0 --- 表示关机级别（不要将默认的运行级别设置成0）
* 1 --- 单用户模式
* 2 --- 多用户模式，不带 NFS （Network File System），没有网
* 3 --- 多用户模式，完全的多用户模式，multi-user.target: analogous to runlevel 3
* 4 --- 没有内使用的模式（被保留模式）
* 5 --- X11，完整的图形化界面模式，graphical.target: analogous to runlevel 5
* 6 --- 表示重启级别（不要将默认的运行界别设置成6，设置后重启）

与运行级别相关命令，该命令调用 init 进程，将运行级别传递给进程，init 指令需要超级管理员权限：
* #init 0 --- 关机
* #init 3 --- 切换到不带桌面的模式，临时切换
* #init 5 --- 切换到图形界面
* #init 6 --- 重启电脑
 
 #### 用户与用户组管理
 linux 系统是一个多用户多任务的操作系统，任何一个要使用系统资源的用户，都需要首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。
 用户的账号一方面可以帮助系统管理员对使用系统的用户进行追踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。
 要实现用户账号的管理，需要完成：
 * 用户账号的添加、删除、修改以及用户密码的管理
 * 用户组的管理

用户管理涉及到三个文件：
* /etc/passwd ：存储用户的关键信息
* /etc/group : 存储用户组的关键信息
* /etc/shadow : 存储用户的密码信息

#### 用户管理
1.添加用户
* #useradd 选项 用户名
	* -g ：表示指定用户组，值可以是用户组的id，也可以是组名 ；
	* -G ：表示用户的用户附加组
	* -u ：uid，用户的id（用户的标识符），不设置系统默认分配
	* -c ：添加注释，如 #useradd -g 501 -G 500 -u 666 lisi
	* 添加后查看：#tail -1 /etc/passwd,显示test1:x:1001::/home/test1:/bin/bash
		* 用户名:密码:用户ID:用户组ID:注释:家目录:解释器shell , 如果用户组已存在是不会显示的，需查看/etc/group
		* 不添加选项是，执行useradd会 创建同名的家目录；创建同名的用户组

2.修改用户
* #usermod 选项 用户名
	* -g 用户主组；-G 用户附加组；-u 用户id；-l 修改用户名
		* #usermod -g 500 -G 501 -l test1 zhangsan
	* -s 修改用户shell，#usermod -s /sbin/nologin test ，test 不能登录系统

3.设置密码
* #passwd 用户名 
	* #passwd zhangsan
* 切换用户命令： #su [用户名] ，不指定用户名表示切换到 root 用户

4.删除用户
* #userdel 选项 用户名
	* -r ：删除用户的同时，删除家目录；
		* 已经登录的用户不能删除，可以 #ps -ef | grep zhangsan 查看 pid ，然后 #kill pid 杀掉进程，再进行删除
	* 删除用户的权限只有 root 用户

#### 用户组管理
查看用户组 #tail -1 /etc/group ，文件结构是  用户组名:密码:用户组ID:组内用户名 ，一般情况下不设置用户组密码，组内用户名表示附加组是该组的用户名称

1.用户组添加
* #groupadd 选项 用户组名
	* -g ：类似用户管理里的 -u ，表示设置一个用户组ID
		* #groupadd Administrators

2.用户组修改
* #groupmod 选项 用户组名
	* -g ：类似 -u，用户组 ID，#groupadd -g 1000 Administrators
	* -n ：类似用户管理里的 -l ，修改用户组名 #groupmod -n admins Administrators

3.用户组删除
* #groupdel 用户组名，#groupdel admins
	* 如果删除的组是某用户的主组时，不允许删除；可以先从组内移除所有用户  `#usermod -g 0 admin`

#### 网络设置
网卡配置文件位置：/etc/sysconfig/network-scripts
在目录中网络的配置文件命名格式：ifcfg-网卡名称 ，其中 ONBOOT 表示是否开机启动，BOOTPROTO 表示 ip 地址分配方式、DHCP 表示动态主机分配协议，HWADDR 表示硬件地址

重启网卡：#service network restart ，有的版本不支持，但有一个共性的目录：/etc/init.d 放着对服务的快捷方式。
* /etc/init.d/network restart

创建快捷方式：
* 软链接：#ln -s 原始文件的路径 快捷方式的路径，#ls -l 查看到的lrw..中的l表示连接

重启单个网卡：
* 停止某个网卡：#ifdown 网卡名，#ifdown eth0
* 开启某个网卡： #ifup 网卡名，#ifup eth0

#### ssh 服务
ssh（secure shell，安全外壳协议），作用：远程连接协议和远程文件传输协议。默认端口22。配置文件位置：/etc/ssh/ssh_config

端口号修改注意：单口范围 0-65535；不能使用已占用的端口。

服务启动/停止/重启：
* service sshd start/stop/restart
* /etc/init.d/sshd start/stop/restart

1.远程终端
终端工具常用的：Xshell、secureCRT、Putty 

2.SSH 服务文件传输工具：FileZilla 。新建站点的时候协议需要选择：SFTP-SSH...

3.设置主机名
* 获取主机名：#hostname ， #hostname -f （FQDN全限定域名）
* 临时设置主机名：#hostname 设置的主机名，设置之后需要切换用户生效 #su
* 永久设置主机名（需重启），主机名配置文件位置，/etc/sysconfig/network
	* 设置主机名为临时主机名就成为永久的：NETWORKING=yes  HOSTNAME=localhost
* 修改linux服务器的 hosts 文件，将修改的主机名指向本地（设置FQDN） hosts 文件的位置 /etc/hosts：直接在该文件添加主机名
	* 不设置 FQDN 有的软件不能启动；影响本地域名解析

#### chkconfig
相当于 windows 下安全辅助工具提供开机启动项的管理服务。在 linux 下不是所有的软件安装完成后都有开机启动服务，有的需要自己添加。

1.开机启动服务查询：#chkconfig --list
* 其中0-6表示各个启动级别，比如 httpd ，其 3 级别关闭，表示其在 3 启动形式下默认开机不启动；5 关闭表示桌面环境下也不启动

2.删除服务：#chkconfig --del 服务名 ，#chkconfig --del httpd

3.添加开机启动服务：#chkconfig --add 服务名 ，有的软件没有服务名，没有服务名的不能运行 service 命令，添加无意义

4.设置服务在某个级别下开机启动/不启动：
* #chkconfig --level 连在一起的启动级别 服务名 on/off ，#chkconfig --level 35 httpd on，#chkconfig --level 5 httpd off

#### ntp 服务
ntp 主要用于对计算机的时间进行同步管理的操作。
同步服务器时间方式有两种：一次性同步（手动同步）和通过服务自动同步。时间上游同步。

1.一次性同步：#netdate 时间服务器的域名或ip地址，#netdate 120.25.108.11

2.设置同步时间服务，服务名 ntpd
* 启动服务：#service ntpd start    或   /etc/init.d/ntpd start
* 设置开机启动服务：#chkconfig --level 35 ntpd on

#### 防火墙服务
防范一些网络攻击。在 centos 中防火墙有一个名称：iptables，7.x 中默认使用的是 firewalld。

1.查看 iptables 是否开机启动：
* 方法1：#ps -ef | grep iptables
* 方法2：#chkconfig --list | grep iptables

2.iptables 服务启动/重启/关闭
* service iptables start/restart/stop
* /etc/init.d/iptables start/stop/restart  或  /bin/systemctl stop firewalld

3.查看 iptables 的状态
* #service iptables status 

4.查看规则的命令
* #iptables -L -n ，-L表示列出队则，-n表示将单词表达形式改成数字形式显示

5.简单设置防火墙规则
* iptables -A INPUT -p tcp --dport 80 -j ACCEPT #允许访问80端口
* iptables -A INPUT -p tvp --dport 20 -j ACCEPT #运行FTP服务的20端口
* iptables -A INPUT -j reject #禁止其他为允许的规则访问
	* iptables 主命令；-A 添加规则，-p 制定协议；--dport 制定端口；INPUT 进站请求；-j 制定行为结果ACCEPT（允许）/禁止（reject）
* 添加完成之后需要保存操作：/etc/init.d/iptables save

#### rpm 管理
类似与 windows 中的软件管理，对 linux 服务器上的软件包进行对应管理：查询、卸载、安装。

1.查询软件是否安装
* #rpm -qa | grep 关键词
	* -q 查询，-a 全部；#rpm -qa | grep firefox

2.卸载软件
* #rpm -e 软件关键词；卸载火狐 #rpm -e firefox 
	* 当被卸载软件存在以来关系时不能卸载，可以使用以下命令忽略依赖关系：#rpm -e httpd --nodeps

3.软件安装
* 软件安装需要先获得软件包：a.去官网下载；b.从光盘或镜像文件中读取 #lsblk，查看光盘/U盘等
* 光盘的挂载和解挂
	* 解挂：#umount 当前设备的挂载点（路径），相当去移除U盘
	* 挂载：#mount 设备原始地址 要挂载的位置路径
		* 设备原始地址同意在/dev下，然后根据大小确定name，拼凑在一起例如："/dev/sr0"
		* 要挂载的位置路径：统一挂载在mnt下，如”/mnt/dvd“，没有就创建   
* 安装软件的命令：#rpm -ivh 软件包完整名称
	* -i 安装，-v 显示进度条，-h 以#显示进度条

#### cron / crontab 计划任务
在指定的时间点去执行任务。
语法：#crontab 选项
* 常用选项：
	* -l ：list，列出指定用户的计划任务列表
	* -e ：edit ，编辑指定用户的计划任务列表
	* -u ：user ，指定的用户名，如果不指定，则是当前用户
	* -r ：remove ，删除指定用户的计划任务列表
* 编辑计划任务：计划任务语法格式以行为单位，一行为一个计划
	* 分 时 日 月 周 需要指定的命令，周0（星期天）~6
		* * ： 表示取值范围内每一个数字
		* - ： 做连续区间表达式的，想要表示1~7，则写成：1-7
		* / ： 表示每多少个，例如每10分钟一次，*/10
		* , ： 表示多个不连续取值，例如1点2点6点，1,2,6
	* 每月1、10、22日的4:45重启network服务： 45 4 1,10,22 * * service neteork restart
	* 每周六、周日的1:10重启netwrok服务：10 1 * * 6,0 service network restart
	* 每天18:00至23:00每隔30分钟重启network服务：*/30 18-23 * * * service network restart
	* 每隔两天的上午8点到11点的第3和第15分钟执行一次重启：3,15 8-11 */2 *  * reboot

crontab 权限问题，配置文件在：/etc/cron.deny ，在该文件内添加用户名，就能不允许该用户配置。在 /etc/cron 创建 cron.allow 文件，添加用户名该用户为白名单用户，白名单用户级别高于黑名单。

### 权限管理
linux 的权限操作与用户、用户组有关。在多用户（可以不同时）计算机系统的管理中，权限是指某个特定的用户具有特定的系统资源使用权力。linux 系统一般将文件可存/取访问的身份分为3个类别：owner、group、others，且3中身份各有read、write、execute等权限。

owner （文件所有者，默认为文档的创建者），group （与文件所有者同组的用户），others （其他人，相对于所有者）。在 linux 中，可以使用 #ls -l 查看文件的属性。

`drwxr-x---`其中的 d 表示文件类型文件夹，rwx 表示文件所有者的权限且位置顺序不会变，r-x 表示文件所属用户组权限，--- 表示其他人对这个文档的权限。r 表示可读，w 可写，x 可执行，- 没有对应权限或表示文件，l 表示软连接。

#### 权限设置
语法：#chmod 选项 权限模式 文档
常用选项，要给文档设置权限，操作者要么是 root 用户，要么是文档所有者：
* -R ：递归设置权限（当文档类型为文件夹的时候设置）
* 权限模式：需要设置的权限信息
* 文档：文件或文件夹。路径可以是相对路径和绝对路径

1.字母形式设置权限：
* 给谁设置：u 表示所有者身份，g 表示所有者同组用户，o 给其他用户设置，a 给所有人设置权限。默认是 a
* 权限字符：r、w、x
* 权限分配方式：+ 表示给具体用户新增权限，- 删除权限，= 将权限设置成具体的值 
给 tt.txt 文件（-rw-------）设置所有者拥有全部权限，同组用户拥有读和执行权限，其他用户只读权限。
* #chmod u+x,g+rx,o+r tt.txt 或 #chmod u=rwx,g=rx,o=r tt.txt 

2.数字形式
#chmod 777 tt.txt，r 等于 4，w 等于 2，x 等于 1 ，- 等于 0.
不能设置只能写不能读的权限，不能设置为 2 或者 3 .

3.注意事项：在 linux 中如果要删除一个文件，不是看文件有没有对应的权限，而是看文件所在的目录是否有写权限，如果有才可以删除。

#### 属主与属组设置
属主：所属的用户（文档的主人）；属组：所属的用户组。
`2 root root 0`前一个 root 表示属主，后一个表示属组。在文档创建的时候会使用创建者的信息（用户名、用户所属的主组名称）

1.chown ：更改文档的所属用户
* 语法： #chown [-R] username 文档路径
* 将 root 用户创建的 oo 目录，所有者更改为 test：#chown test oo/ 

2.chgrp ，更改文档的所属用户组
* 语法： #chgrp [-R] groupname 文档路径
* 将 root 创建的 oo 目录所有者改为 test，并将所属用户组也改为 test： #chgrp test oo/

3.chown 还可以同时修改所属用户和所属用户组
* 语法： #chown [-R] username:groupname 文档路径
* 将 oo 目录的所属用户和用户组改回成 root ，并且包含其子目录：#chown -R root:root oo/

#### 其他
reboot、shutdown、init、halt、user管理，在普通用户身份都是操作不了，但是有时又需要有执行权限，并且不可能让 root 用户把自己的密码告诉普通用户。可以使用sudo命令来进行权限设置，sudo 可以让管理员（root）事先定义某些特殊指令谁可以执行。

默认 sudo 中时没有除 root 之外用户的规则，要想使用则需要先配置 sudo，sudo配置文件位置：/etc/sudoers 。
* 配置 sudo 文件需使用“#visudo”打开配置文件，使用方式与vim一致
* 配置普通用户的权限，找到配置文件中的：root ALL=(ALL) ALL
	* root 表示用户名；ALL 表示允许登录的主机（地址白名单）；（ALL）表示以谁的身份执行，ALL表示 root 身份；ALL 表示当前用过户可以执行的命令，多个命令可以使用“,”分割。
* 本身 test 用户不能添加用户，使用 sudo 配置将其配置为能以 root 身份进行添加用户和设置密码（但不能修改 root 用户密码）
	* #visudo ，打开配置文件；在 sudo 规则的时候不建议写直接形式的命令，而是写命令的完整路径。路径可以使用 which 命令来查看，#which 指令名称，如#which useradd
	* 在配置文件中添加，禁止修改 root 密码的配置： test ALL=(ALL) /usr/sbin/useradd, /usr/bin/passwd [A-Za-z]*,!/usr/bin/passwd root
	* 在添加好对应的规则后就可以切换用户，切换到普通用户 test 再去执行：#sudo 需要执行的指令，#sudo useradd aop
	* 普通用户查看自己的权限：#sudo -l

:!which useradd  ==>> /sbin/useradd
:!which passwd ==>> /bin/passwd

### linux 中的计算机网络

#### 网络概述
1969年ARPANET（美国成立的国防部高级研究计划署）开始联机，该年被成为 Internet 元年。网络分类：局域网（LAN）、城域网（MAN）、广域网（WAN）。网络按照所有者划分为公网和私网。

1、IP 地址
IP 地址，ip即 internet protocol 网络之间互联的协议。IP 地址按类型分为：公有地址和私有地址。
公有地址（public address）由 Inter NIC（因特网信息中心）负责，将 IP 地址分配给注册并向 Inter NIC 提出申请的组织机构，通过它直接访问因特网。
私有地址（private address）属于非注册地址，专门为组织机构内部使用。以下时留用的内部私有地址分类：
* A 类 ：10.0.0.0 -- 10.255.255.255
* B 类 ：172.16.0.0 -- 172.31.255.255
* C 类 ：192.168.0.0 -- 192.168.255.255

IP 地址按类型分为三类：

|  类别   |  最大网络数   |   IP 地址范围  |  最大主机数   |   私有 IP地址分配  |
| --- | --- | --- | --- | --- |
|  A   |  126(2^7 - 2)   |  1.0.0.0 -- 127.255.255.255   |  16777214   |  10.0.0.0 -- 10.255.255.255   |
|  B   |  16384(2^14)   |  128.0.0.0 -- 191.255.255.255   |  65534   |  172.16.0.0 -- 172.31.255.255   |
|  C   |  2097152(2^21)   |  192.0.0.0 -- 223.255.255.255   |  254   |  192.168.0.0 -- 192.168.255.255   |

2、网卡
网卡时一个网络组件，主要负责计算机之间数据的封装和解封。MAC 地址：网卡的物理地址，网卡设备的编号，默认情况是全球唯一的（16进制的）。与 IP 地址的区别：长度不同，IP 地址为 32 位，MAC 地址为 48 位；分配依据不同；网络寻址方式不同，OSI 参考模型中 IP 地址是在网络层，MAC 地址是在数据链路层。

3、网线，在局域网中常见的网线主要有双绞线（RJ45 接口）、同轴电缆、光缆三种。

4、交换机，是一种用于光电信号转发的网络设备，可以位接入交换机的任意两个网络节点提供独享的电信号通路。集线器是共享带宽的平分。常见交换机品牌华为、华三、思科、锐捷。

5、路由器，又称网关设备（Gateway），用于连接多个逻辑上分开、相对独立的网络。

6、拓扑结构图，拓扑就是把实体抽象成其大小、形状无关的点，而把连接实体的线路抽象成线，进而以图的形式来表示这些点与线之间关系的方法，目的在于研究点、线之间的相连关系。表示点和线之间关系的图被称为拓扑结构图。常见的拓扑结构图有：星型拓扑结构、总线型拓扑结构、环形拓扑结构、树形拓扑结构、网状拓扑结构、混合型拓扑结构、蜂窝网络结构。

#### 网络相关命令
1、ping，检测当前主机与目标主机之间的连通性
语法：#ping 主机地址(ip 地址、主机名、域名等)，如 #ping www.baidu.com

2、netstat，查看网络的连接信息
语法：
* #netstat -tnlp，-t tcp协议，-n 将字母转换成数字，-l 列出状态为监听的，-p 显示进程相关信息
* #netstat -an，-a 表示全部，-n 将字母转化成数字

3、traceroute，查找目前主机与目标主机之间所有的网关（路由器，会给沿途各个路由器发送 icmp 数据包，路由器可能会不给响应）。该命令不是内置命令，需安装。
语法：#traceroute 主机地址  

4、arp，地址解析协议ARP，是根据 IP 地址获取（MAC）物理地址的协议。
语法：
* #arp -a，查看本地缓存 MAC 表
* #arp -d 主机地址，删除指定的缓存记录

5、tcpdump，抓包，抓取数据包
语法：
* #tcpdump 协议 port 端口，#tcpdump port 22
*  #tcpdump 协议 port 端口 host 地址
*   #tcpdump -i 网卡设备名

#### 上线流程
1、服务器选配
项目上线服务器必须是外网服务器，一般服务器有2中情况，购买真实服务器（成本高）、购买云服务器（主流）。云服务的厂商，阿里云、腾讯云、知道创宇（加速乐）、华为云、盛大云、新浪云、亚马逊云等等。 

步骤：
1. 打开阿里云官网，[阿里云](https://www.aliyun.com/)，选择产品中的“云服务器 ECS”，点击立即购买。
2. 选择具体配置：地域、IO等然后购买
3. 进入后台查看信息，更多里面选择“重置密码”，然后重启服务器，通过远程终端工具就能连接了。

2、域名购买
步骤：
1. 在产品中选择域名购买，输入想要注册的域名，查看是否可以注册
2. 选择需要的域名，点击结算
3. 购买成功在后台域名中查看信息

3、域名备案，当申请域名的人想要在国内使用域名，则需要向当地的通信管理局（省级）去申请报备。备案前提：需要使用境内服务器，必须备案。
在管理后台点击备案---ICP备案系统，点击新增主体备案，填写完信息后点击增加网站，其中的备案服务号需要在备案--备案服务号申请中申请；申请到备案号之后，会让用户下载一个图片--网站真实性核验单，下载打印填写好上传到阿里云备案系统中，后面等待初审，初审通过后继续下一步，需要拍照，上传照片等待管局审核，通过后会收到工信部发送的短信与邮件通知，里面有备案号和备案密码（用于注销备案）。

4、域名解析，将域名绑定到一个服务器地址的操作，后台中点击解析。当在浏览器中输入一个域名，会向发送请求到 DNS Server，将域名转换成 IP 地址的服务器。点击添加解析，记录类型中A-将域名指向一个IPV4地址，CNAME-将域名指向另一个域名，MX-将域名指向邮件服务器地址；记录值是服务器的 IP 外网地址。

5、配置生产环境

6、上传代码，需要用到上传工具。

### Shell 基础
Shell（外壳）是一个用 C 语言编写的程序，它是用户使用 linux 的桥梁，既是一种命令语言，又是一种程序设计语言。shell 是指一种应用程序，这个应用程序提供一个界面，用户通过这个界面访问操作系统内核的服务。
脚本就是一条条的文字命令，这些文字命令是可以看到的。常见的脚本：javascript、vbscript、asp、jsp、php、sql、perl、shell、python、ruby、javafx、lua等。
shell 是内置的脚本，程序开发的效率高。（批处理）语法简单易学。linux 中默认的 shell 是 /bin/bash，流行的 shell 有 ash、bash、ksh、csh、zsh等。 bash 可以使用 #help 查看帮助。

shell 脚本分为简单的写法（命令的堆积）和复杂的写法（程序设计）。

#### shell 规范
1.编写规范：
```
# 代码规范
#!/bin/bash    [指定告知系统当前这个脚本要使用的 shell 解释器]
shell 相关命令

# 命名规范
文件名.sh    .sh 是 linux 下 bash shell 的默认后缀
```
2.使用流程：创建 .sh 文件 -->> 编写 shell 代码 -->> 执行 shell 脚本，必须要有执行权限 #chmod +x test.sh。运行的时候需要写成 #./test.sh 或 #/root/test.sh 或 /bin/bash test.sh，linux 系统中的 PATH 环境变量存在路径是 /bin，/sbin，/usr/bin，/usr/sbin 等。
```
#!/bin/bash
echo 'hello world!'
```

#### 变量
1.变量的定义和使用
* 变量的定义(字母、下划线和数字)： class_name=“hello world” 
* 变量的使用： echo $class_name 
* echo "$class_name" 与 echo '$class_name'
	* 双引号能识别变量，实现转义；单引号不能识别变量，原样输出
* 变量的值是命令需要使用反引号：dt=`date +'%F %T'`

2.只读变量
语法：readonly 变量名；a=10  readonly a  a=20  echo a -->> 10

3.接受用户输入
语法：read -p 提示信息 变量名，变量名用于保存输入
```
#!/bin/bash
## 提示用户输入文件的名称，自动创建文件
read -p '请输入需要创建的文件路径：' filepath
touch $filepath
echo '文件创建成功'
ls -l $filepath
```

4.删除变量
语法：unset 变量名，b=20; echo b; unset b; echo b; -->> 20

#### 条件判断
```
## 语法1：if...then
if [ condition ]
then
    command1
	command2
	...
fi
## 单行写法，一般在命令行中执行
if [ condition ];then command;fi

## 语法2：if...then...else
if [ condition ]
then 
    command1
	command2
	...
else
    command
fi

## 语法3：if...then...elif...then...fi
if [ condition1 ]
then
    command
elif [ condition2 ]
then
    command
else
    command
fi
```

#### 运算符
在 shell 中除了常见的算数运算符、关系运算符、逻辑运算符、字符运算符，还有文件测试运算符等。

原生 bash 不支持简单的数学运算，但可以使用命令来实现，例如 awk 和 expr 。
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。
文件测试运算符用于检测 Unix/Linux 文件的各种属性。

|   运算符  |  说明   |   举例  |
| --- | --- | --- |
|  算数运算符   |     |     |
|  +   |  加法   |  `expr $a + $b`，表达式和运算符之间要有空格，完整的表达式要被 `反引号`包含   |
|  -   |  减法   |  `expr $a - $b`  |
|  *   |  乘法   |  `expr $a \* $b`   |
|   /  |  除法   |  `expr $a / $b`  |
|  %   |  取余   |  `expr $a % $b`  |
|  =   |   赋值  |  a=$b   |
|  ==   |  相等，用于比较两个数字，相同为 true   |  [$a == $b] ，条件判断要放在方括号中，并且有空格  |
|  !=   |   不想等，用于比较两个数字，不相同为 true  |  [$a != $b]    |
|  逻辑运算符   |     |     |
|  -eq   |  检测两个数是否相等，相等为 true   |  [ $a -q $b ]   |
|  -ne   |  检测两个数是否相等，不想等为 true   |  [ $a -ne $b ]   |
|  -gt   |  检测左边的数是否大于右边的，大于为 true   | [ $a -gt $b ]    |
|  -lt   |  检测左边的数是否小于右边的，小于为 true   |  [ $a -lt $b ]   |
|  -ge   |  检测左边的数是否大于等于右边的，是为 true   |  [ $a -ge $b ]   |
|  -le   |  检测左边的数是否小于等于右边的，是为 true   |  [ $a -le $b ]    |
|  !   |  非运算，表达式为 true 返回 false   |  [ !false ] 返回 true  |
|  -o   |  或运算，有一个表达式为 true 则返回 true   |  [ $a -lt 20 -o $b -gt 100 ]   |
|  -a   |  与运算，两个表达式都为 true 才返回 true   |   [ $a -lt 20 -a $b -gt 100 ]  |
|  字符串运算符   |     |     |
|  =   |   检测字符串是否相等，相等返回 true  |  [ $a = $b ]   |
|  !=   |  检测两个字符串是否相等，不想等返回 true   |  [ $a != $b ]   |
|  -z   |  检测字符串长度是否为 0，为 0 返回 true   |  [ -z $a ] ，a 是数值会返回 true   |
|  -n   |  检测字符串长度是否为0，不为 0 返回 true   |  [ -n $a ]   |
|  str   |  检测字符串是否为空，不为空返回 true   |  [ $a ]   |
|  文件测试运算符   |     |     |
|   -b file  |  检测文件是否是块设备，如果是返回 true   |  [ -b $file ]，块设备像 U盘、光盘这些   |
|  -c file   |  检测文件是否是字符设备文件，如果是返回 true   |  [ -c $file ]   |
|  -d file   |  检测文件是否是目录，如果是返回 true   |  [ -d $file]   |
|  -f file  |  检测文件是否是普通文件（既不是目录也不是设备文件），如果是返回 true  |  [ -f $file ]  |
|  -q file  |  检测文件是否设置了 SGID 位，如果是返回 true  |  [ -q $file ]  |
|  -k file  |  检测文件是否设hi在了粘着位(Sticky Bit)，如果是返回 true  |  [ -k $file ]  |
|  -p file  |  检测文件是否是有名管道，如果是返回 true  |  [ -p $file ]  |
|  -u file  |  检测文件是否设置了 SUID 位，如果是返回 true  |  [ -u $file ]  |
| -r file   |  检测文件是否可读，如果是返回 true  |  [ -r $file ]   |
|  -w file   |  检测文件是否可写，如果是返回 true  |  [ -w $file ]   |
|  -x file  |  检测文件是否可执行，如果是返回 true  |  [ -x $file ]   |
|  -s file  |  检测文件是否为空（文件大小是否小于0），不为空返回 true  | [ -s $file ]    |
|  -e file  |  检测文件（包括目录）是否存在，如果是返回 true  |  [ -e $file ]   |

#### shell 脚本附带选项
在 shell 中如果处理 tail -10 /etc/passwd 这样的命令行：
步骤：先调用 tail 指令；然后系统把后续选项传递给 tail；tail 先去打开指定的文件；最后取出最后 10 行。

自定义 shell 像内置命令一样值传递，传递方式与上述一样，需要定义接受参数。
传递：#./test.sh a b c
接收：在脚本中可以用”$1“表示 a，“$2”表示 b，“$3”表示 c，以此类推。即可以用“$”加上选项对应的序号进行接收，"$0"表示文件自身./test.sh。
```
#!/bin/bash
# 自定义指令'user',可以使用#user -add 用户名，添加用户；#user -del 用户名，删除用户及其家目录
if [ $1 = '-add' ];then
    useradd $2
else
   userdel -r $2
fi

-->>然后在控制台添加:#./test.sh -add aaa，删除：#./test.sh -del aaa
--->>可以配置别名文件 vim ~/.bashrc，添加 alias user='/root/test.sh'，切换用户#su生效
--->>就可以使用#user -add aaa进行添加用户了
```

### linux 下的 MySQL
1.安装方式
a. 源码包形式，使用源码编译安装方式安装 ncurses （一种常用的终端库）
```
解包常用语法：
		#tar -zxvf *.tar.gz    
		#tar -jxvf *.tar.bz2
选项含义：
		-z 或 --ungzip ：通过 gzip 指令处理文件
		-x 或 --extract 或 --get ：从文件中还原文件
		-v ：显示操作过程
		-f 或 --file ：指定一个文件
		-j ：支持 bzip2 解压文件
``` 
步骤：
* 上传压缩包到服务器指定路径，比如 /usr/local/src
* 解压源码包： #tar -zxvf ncurses-6.1.tar.gz
* 进入到解压的文件夹，进行后续配置等操作
	* 配置（配置文件名常为 config | configure | bootstrap）-> 编译（make | bootstrap）-> 安装（make install | bootstrap install）
	* 配置需指定软件的安装目录、需要依赖的位置、指定不需要可选以来、配置文件路径、通用数据库存储位置等等
		* 指定安装的路径：--prefix=路径，如#./configure --prefix=/usr/local/ncurses
		* 需要依赖的路径： --with-PACKAGE 名=包所在的路径
		* 不需要依赖：--without-PACKAGE 名
	* 编译：#make
	* 安装：#make install

b. 二进制包形式（rpm）
指令：
* #rpm -qa | grep 关键词 ，查询安装的情况
* #rpm -e 关键词 [--nodeps] ，卸载安装[是否忽略依赖关系]
* #rpm -ivh 完整名称，安装软件需要完整的包名
* #rpm -Uvh 完整名称，完整名称可以是http路径，升级软件包
* #rpm -qf 文件路径 ，查询指定文件属于哪个包,#rpm -qf /etc/httpd/conf/httpd.conf
使用二进制包安装 lynx（一款纯命令行的浏览器），安装包的文件后缀名是 .rpm 的。#lynx --dump www.baidu.com，访问百度。

c. yum 等傻瓜式安装，不更改来源的情况下默认需要联网的。
常用 yum 指令：
* #yum list ，列出本机已经装的和可以装的软件
* #yum search 名，搜索是否有可用安装包
* #yum [-y] install 包名，-y 可以避免安装的时候提示是否确认安装
* #yum [-y] update [包名]，更新指定的包，不指定就更新全部的包
* #yum [-y] remove 包名，卸载指定的包

2.安装 mysql
在安装包之前可以先更新以下#yum update，然后添加 EPEL 源，这个为“红帽系”的操作系统提供额外的软件包。比如：
* rpm -ivh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-10.noarch.rpm ，安装epel-release
* rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm ，安装PHP7的rpm源
* rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm ，安装mysql源
* #yum install mysql-server，是安装服务端的包，不是安装客户端的
	* #yum install mysql-community-server.x86_64，安装 mysql5.6

3.mysql 初始化
* #service mysqld start ，开启mysql服务
	* #netstat -tnlp ，查看端口号，mysql 默认端口号 3306
* #mysql_secure_installation
	* Enter current password for root (enter for none): 第一次设置直接 enter 设置密码
	* Remove anonymous users? [Y/n] 是否移除匿名用户，选择Y
	* Disallow root login remotely? [Y/n] 不允许 root 远程登陆，n
	* Remove test database and access to it? [Y/n] 是否移除测试数据库，n
	* Reload privilege tables now? [Y/n] 是否重新加载权限表，当更改了mysql用户相关信息是 Y

设置了能远程登陆可能存在不能远程登陆的情况，需要修改用户表里的数据：
* mysql> SELECT host,user FROM user;  # 查询所有用户情况
* mysql> UPDATE user SET host='%' WHERE host='localhost.localdomain'
* 最后刷新权限表或者重启 mysql
	* mysql> flush privileges;

4.mysql 启动：#service mysqld start | stop | retart
* 进入 mysql 的方式： #mysql -u 用户名 -p

5.mysql 默认目录/文件位置
数据库存储目录：/var/lib/mysql
配置文件：/etc/my.cnf

6.备份与还原
a. 备份
```
全量备份（数据和结构）：#mysqldump -u root -p 密码 -A > 备份文件路径.sql
指定库备份（数据和结构）：#mysqldump -u root -p 密码 库名 > 备份文件路径.sql
多个库备份（数据和结构）：#mysqldump -u root -p 密码 --databases db1 db2 >备份文件路径.sql

# 计划任务，比如每隔 1 分钟备份一次数据库
#!/bin/bash
filename="test"`date +'%Y$m%d%H%M%S'`".sql"
mysqldump -uroot -padmin@123 -A > /root/$filename
#corntab -e
# 分 时 日 月 周 命令
* * * * * /root/test.sh
```
b. 还原
```
还原部分分为：mysql 命令行 source 方法和系统命令方法
1.还原全部数据库：
（1）mysql 命令行：mysql> source 备份文件路径
（2）系统命令行：#mysql -uroot -padmin@123 < 备份文件路径
2.还原单个数据库（需指定数据库）
（1）mysql> use 库名
		 mysql> source 备份文件路径
（2）mysql -uroot -padmin@123 库名 < 备份文件路径

设置临时 mysql 连接字符集：mysql>SET NAMES utf8;
```
7.mysql 的远程管理工具
分为两大类：B/S 架构 和 C/S 架构。在 B/S 中有 PMA（phpMyAdmin）; C/S 中有 navicat 等。

### 网站运维
#### 编译安装与卸载 Nginx
Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在BSD-like 协议下发行。类似与 apache，其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

1.安装 nginx，[官网](http://nginx.org/)
（1）使用在服务器端下载的方式进行下载：
* #wget 地址
	* 例如要下载 nginx 到 “/usr/local/src”，右键复制官网 tar 包链接地址
	* #wget -P /usr/local/src http://nginx.org/download/nginx-1.15.12.tar.gz
（2）解压 nginx 安装包
* #tar -zxvf nginx-1.15.12.tar.gz
（3）进入解压目录，配置、编译、安装
* #./configure --prefix=/usr/local/nginx  ，指定安装路径
	* 如果配置时报错没有 PCRE 库，#yum install pcre-devel，然后 #./configure --prefix=/usr/local/src --with-pcre
	* 如果报错缺少 zlib 库，#yum install zlib-devel ，然后 #./configure --prefix=/usr/local/src --with-pcre --with-zlib=/usr/local/src/包名
* #make ，编译
* #make install ，安装

2.运行 nginx，因为 apache 默认占用端口是 80，nginx 占用的也是 80，所以直接启动 nginx 是启动不起来的，需关闭 apache，#service stop httpd
* 开启 nginx 服务：#/usr/local/nginx/sbin/nginx
* 重启/重载配置文件：#/usr/local/nginx/sbin/nginx -s reload

3.卸载编译安装的软件
* #rm -rf 软件的安装路径，卸载一个编译安装的软件的时候必须先停止。

#### 关于 LAMP
LAMP = Linux + Apache + MySQL +PHP
LNMP = Linux + Nginx + MySQL + PHP-fpm
LNMAP = Linux + Nginx + MySQL + PHP + Apache

登录阿里云控制台获取需要连接的主机 ip 地址，用于远程登录。

1.PHP 与 Apache 的安装
* 先装 PHP 在安装的时候会顺带安装 Apache：#yum install php
	* 如果启动 apache 警告无法确定 FQDN 需要修改 apache 配置文件(/etc/httpd/conf/httpd.conf):#vim /etc/httpd/conf/httpd.conf
		* 搜索 /ServerName，去掉 ServerName www.example.com:80 注释，重启就可以了

测试 apache 在浏览器中输入 ip 地址能运行 apache 测试页面就可以了。
测试 PHP （默认的 apache 站点目录：/var/www/html）：创建一个 test.php 文件，添加代码 <?php phpinfo(); ?>
* 如果页面刷新显示是代码，则需要配置 /etc/httpd/conf/httpd.conf，配置完成后需要重启 apache 服务。


```
<Directory />
    AllowOverride none
    Require all denied   --- >>>  Require all granted
</Directory>

AddType application/x-gzip .gz .tgz
# 下面添加一行
AddType application/x-httpd-php .php

<IfModule dir_module>
    DirectoryIndex index.html -->> DirectoryIndex index.html index.php
</IfModule>
```

2.安装 mysql ：#yum install mysql-server
阿里云后台相关的端口需要打开，比如 80 ，3306

3.项目上线
上传文件，如果配置的时候显示不支持 mysqli_connect()，则需要 mysqli 扩展：#yum install php-mysqli

### VMware
vmware为我们提供了三种网络工作模式，它们分别是：Bridged（桥接模式）、NAT（网络地址转换模式）、Host-Only（仅主机模式）。
打开vmware虚拟机，我们可以在选项栏的“编辑”下的“虚拟网络编辑器”中看到VMnet0（桥接模式）、VMnet1（仅主机模式）、VMnet8（NAT模式），那么这些都是有什么作用呢？其实，我们现在看到的VMnet0表示的是用于桥接模式下的虚拟交换机；VMnet1表示的是用于仅主机模式下的虚拟交换机；VMnet8表示的是用于NAT模式下的虚拟交换机。
同时，在主机上对应的有VMware Network Adapter VMnet1和VMware Network Adapter VMnet8两块虚拟网卡，它们分别作用于仅主机模式与NAT模式下。在“网络连接”中我们可以看到这两块虚拟网卡，如果将这两块卸载了，可以在vmware的“编辑”下的“虚拟网络编辑器”中点击“还原默认设置”，可重新将虚拟网卡还原。

#### Bridged（桥接模式）
桥接模式就是将主机网卡与虚拟机虚拟的网卡利用虚拟网桥进行通信。在桥接的作用下，类似于把物理主机虚拟为一个交换机，所有桥接设置的虚拟机连接到这个交换机的一个接口上，物理主机也同样插在这个交换机当中，所以所有桥接下的网卡与网卡都是交换模式的，相互可以访问而不干扰。在桥接模式下，虚拟机ip地址需要与主机在同一个网段，如果需要联网，则网关与DNS需要与主机网卡一致。其网络结构如下图所示：

![](./images/bridge.png)

设置虚拟机为桥接模式：
1. 选择需要编辑的虚拟机，点击“编辑虚拟机设置”，选择“网络适配器”-->>“桥接模式”。
2. 查看 windows 上网络连接信息，IPv4地址：192.168.0.117，IPv4 默认网关：192.168.0.1，IPv4 DNS 服务器：192.168.0.1
3. 进入系统编辑网卡配置文件，#vim /etc/sysconfig/network-scripts/ifcig-ens33
	* HWADDR= 00：0c：29：92：12：b2 -->> 设置网卡物理地址，查看是 #ip addr
	* IPADDR=192.168.0.120 -->> 设置与主机 ip 地址在同一网段
	* NETMASK=255.255.255.0 -->> 设置子网掩码
	* GATEWAY=192.168.0.1 -->> 设置虚拟机网关，与主机相同
	* DNS1=192.168.0.1 -->> 设置虚拟机DNS，与主机相同
	* BOOTROTO=none -->> 修改默认设置
4. 重启网卡 #service network restart，查看是否联网 #ping www.baidu.com

#### NAT（地址转换模式）
如果你的网络ip资源紧缺，但是你又希望你的虚拟机能够联网，这时候NAT模式是最好的选择。NAT模式借助虚拟NAT设备和虚拟DHCP服务器，使得虚拟机可以联网。其网络结构如下图所示：

![](./images/nat.png)

设置虚拟机为 NAT 模式：
1. 打开 VMware，点击“编辑”下的“虚拟机网络编辑器”，设置 NAT 参数。
	* 选择 VMnet8，先点击“NAT 设置”设置网关 IP，再点击“DHCP 设置”设置“起始 IP 地址”、“结束 IP 地址”、以及“租用时间”。
2. 选择虚拟机，点击“编辑虚拟机设置”，选择“网络适配器”-->>“NAT 模式”。
3. 进入虚拟机编辑网卡配置文件，#vim /etc/sysconfig/network-scripts/ifcig-ens33
	* 注释掉 HWADDR
	* BOOTPROTO=dhcp -->> 动态获取 ip 地址，如果设置为静态，则配置 ip 需要在 DHCP 地址范围内 
	* 不需要手动配置则注释掉：IPADDR、NETMASK、GATEWAY、DNS1
4. 重启网卡 #service network restart，查看是否联网 #ping www.baidu.com
	
#### Host-Only（仅主机模式）
Host-Only模式其实就是NAT模式去除了虚拟NAT设备，然后使用VMware Network Adapter VMnet1虚拟网卡连接VMnet1虚拟交换机来与虚拟机通信的，Host-Only模式将虚拟机与外网隔开，使得虚拟机成为一个独立的系统，只与主机相互通讯。其网络结构如下图所示：

![](./images/host-only.png)

设置虚拟机为 Host-Only 模式：
1. 编辑“虚拟机网络编辑器”，设置 DHCP 的起始范围。
2. 点击“虚拟机设置”，选择“网络适配器”-->>“仅主机模式”
3. 启动系统，设置网卡文件
	* BOOTPROTO=dhcp
	* IPADDR、NETMASK、GATEWAY、DNS1可以注释
4. 重启网卡，测试连接通信。
5. 主机与虚拟机通信之后，如果想要联网，需要将网络分享给网卡。
	* 在“网络适配器”中选择联网的网卡，查看属性，点击“共享”
	* 勾选“允许其他网络用户通过此计算机的...”，并选择网卡"... VMnet1"
6. 设置网卡 "...VMnet1"的 ip 地址为 192.168.93.1，进入系统编辑网卡配置：
	* GATEWAY=192.168.93.1
	* DNS=192.168.93.1
7. 重启网卡 #service network restart，查看是否联网

### 其他

#### 远程管理线上服务器
1、添加用户，添加组，设置权限
* 设置密码除了 passwd，还可以使用 #echo 123|passwd --stdin code1
	* stdin ：标准输入，键盘上输入的内容，0
	* stdout ：标准输出，屏幕上输出的正确的结果，1
	* stderr ：标准错误，屏幕上输出的错误的结果，2
		* ./1.sh >/dev/null 2>/tmp/3.log
		* ./1.sh &>/tmp/4.log 等价于 ./1.sh >/tmp/5.log 2>&1
* 权限分类：普通权限(rwx)、高级权限、默认权限、ACL 控制策略
	* 高级权限：
		* 冒险位(set uid) -- 4000 针对一些命令，临时拥有文件的拥有者权限 
			* #chmod u+s /usr/bin/vim 或 #chmod 4755 /usr/bin/vim
		* 强制位(set gid) -- 2000 一般针对公共目录，用于强制位表示任何用户在该目录下创建的文件的强制继承该目录的属组 
			* #chmod g+s /share/dir 或 #chmod 2755 /share/dir
		* 粘滞位(sticky bit) -- 1000 一般针对公共目录，用于粘滞位表示除了 root 和文件的创建者可以删除自己的文件，其他人只能管理子的的文件
			* #chmod o+t /data/code 或 #chmod 1755 /data/code
```
-- 添加三个开发人员 code1 code2 code3
#useradd code1  #useradd code2  #useradd code3;
-- 添加密码，以此类推
#echo 123|passwd --stdin code1 
-- 添加一个 code 组，并把 code1 等添加到该组，有两种方法
#groupadd code
#usermod -G code code1
#gpasswd -a code2 code  #gpasswd -a code3 code
-- 查看用户信息 
#id code1  或者  #tail /etc/group
-- 创建一个目录/data/code，开发人员能在这里面创建文件
#mkdir -p /data/code 
#chgrp code /data/code  #chmod g+w /data/code
-- 开发人员只能管理自己的文件，不能删除其他人文件
#chmod o+t /data/code/
```
2、线上环境禁止 root 远程登录
（1）scp 命令：远程拷贝
* #scp 需要拷贝的文件 远程服务器，将本地文件拷贝到远程
	* #scp file1 per1@10.1.1.1:/tmp/
* #scp 远程文件 本地路径，将远程文件拷贝到本地
	* #scp -r per1@10.1.1.1:/tmp/dir1 /data/code，-r 递归拷贝
（2）cp 命令：本地拷贝
（3）ssh 客户端工具使用：
* #ssh --help ，#man ssh ，查看帮助
	* #ssh 远程连接的主机ip地址，如 #ssh 10.1.1.1，不指定用户就是当前用户，前提是远程主机有对应用户
	* #ssh 用户名@主机ip地址，如 #ssh per1@10.1.1.1
	* #ssh -l per1 -p 22 10.1.1.1 ， #ssh 10.1.1.1 hostname
（4）查看端口：
* #netstat -tnlp | grep 22 或者 #ss -ntlp | grep 22 或者 #lsof -i :22
（5）禁止 root 远程登录，查看 sshd 服务：
* #rpm -qf /usr/sbin/sshd，查看安装包
* #rpm -ql openssh-server ，查看安装生成哪些文件
	* 其中 ../init.d/sshd 是启动脚本，./sshd_config 配置文件，../sbin/sshd 程序本身
* 禁止远程登录
	* 修改配置文件，#man sshd_config，查看配置文件
	* PermitRootLogin no，找到位置并设置，保存重启服务

3、修改 sshd 服务默认端口为 10022（在生产服务器上修改的）
* 首先查看端口是否被占用，
	* #grep 10022 /etc/services ，#lsof -i 10022，#ss -a|grep 10022 ，#netstat -a|grep 10022
* 修改 sshd 配置文件， Port 10022，重启服务
* 跳板机上登录： #ssh -lper1 10.1.1.1 -p10022
	* 更改 ssh 客户端配置文件不想验证指纹，StrictHostKeyChecking yes，表示直接比对 ~/.ssh/known_hosts 文件中的公钥

4、ssh 免密登录，跳板机上生成一对密钥：公钥 和 私钥。生成之后把 公钥 拷贝到远程主机的 ~/.ssh/ 目录里。
* 生成密钥：#ssh-keygen ，然后回车，id_rsa 私钥，id_rsa.pub 公钥
* 拷贝公钥到远程主机：#ssh-copy-id -i per1@10.1.1.1 或者 #scp id_rsa.pub per1@10.1.1.1:/home/per1/.ssh/authorized_keys

5、rsync 实现数据同步
（1）sync 同步，async 异步，rsync 远程同步。rsync 可以保存原有的权限，owner，group，时间，软硬链接，文件 acl，文件属性信息等。
（2）本地同步：
* #rsync -av /dir1/ /dir2 ，dir1 后面的 / 会影响同步结果，前面是来源，后面是目的地
	* #rsync -av --delete /dir1/ /dir2 ，传出多余的文件
（3）远程同步：
* 同步到远程push： #rsync -avR /dir1/ 10.1.1.1:/backup ，R 同步 dir1 目录及文件
* 本地同步远程pull ：#rsync -avR 10.1.1.1:/backup/app /dir1
（4）rsync 作为后台程序使用
* 创建配置文件：#vim /etc/rsyncd.conf
	* 文件内容： [app_name]   path=/app/project   log file=/var/log/rsync.log
* #rsync --daemon ，启动服务
	* 查看是否启动： #netstat -ntlp | grep 873

#### DNS
DNS（domain name system）域名管理系统，域名是由特定的格式组成，用来表示互联网中某一台计算机或计算机组的名称，能够使人方便的访问互联网。
DNS 作用：
* 域名的正向解析：将主机域名转化为 IP 地址。域名 -->> IP，A 记录
* 域名的反向解析：将 IP 地址转换成域名。IP -->> 域名，PTR 记录
DNS 的结构：
* 根域：在整个 DNS 系统的最上方一定是 .（小数点）这个服务器（称为 root）。
* 一级域名（顶级域 | 国家域）：com edu gov org cc io | cn uk us ru ja ko
* 二级域名：qq.com.   baidu.com.    google.com.