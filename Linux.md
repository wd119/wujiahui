# Linux

## 操作系统

软硬件之间的桥梁

内核提供主要功能 调度硬件

系统程序-调用>内核：Linux发行版

## 虚拟机

虚拟化软件

VMware

### 远程连接linux

finalShell

### 快照

将当前虚拟机的状态保存下来

随时回复快照

## Linux

### Linux目录结构

只有一个根（顶级）目录/，所有文件都在它下面

windows系统 层级关系用\

Linux用/

### linux命令

命令行：Linux终端terminal,是一种命令提示符页面

命令：linux可执行程序

 Linux命令基础格式

command [options] [parameter]

command 命令本身

options 可选 命令的行为细节

parameter可选 命令的指向对象

[]可选

### ls命令

列出目录下的内容

home目录 个人账户目录

ls参数：

> ls [-a]   all列出全部文件

> ls [-l]    以列表（竖向排列）

可以混合使用

ls -al

> ls[-h]  必须结合l 显示文件大小单位

### cd pwd

cd 切换目录

pwd 查看当前工作目录 打印当前工作目录

### 相对路径 绝对路径

绝对路径 以根目录为起点 以/开头

相对目录 以当前目录为起点

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-14%20121751.png)

### mkdir

用来创建文件夹

mkdir [-p] linux路径

参数必须填 

-p可选，表示自动创建不存在的父目录，适用于创建连续多层级目录

*确保操作都在home目录内 在外面涉及到权限问题*

### touch

创建文件

touch Linux路径

### cat命令

查看文件内容

cat linux命令

### more命令

查看文件内容 支持翻页

more Linux路径

按q退出翻页

### cp

用于复制文件、文件夹

cp [-r] 参数1 参数2

-r用于复制文件夹，表示递归

1 被复制的文件

2 复制到的地方

### mv

mv 参数1 参数2

移动文件、文件夹

 不存在即是改名

### rm

rm [-r -f]参数1 参数2.。。。。。。参数n

-r用于删除文件夹

-f强制删除 （不会弹出提示确认信息）

通配符*

test*:表示匹配任何以test开头的内容

*test:表示匹配任何以test结尾的内容

\*test*表示匹配任何包含test的内容

### 查找命令

命令为可执行文件

#### which

查找一系列*命令*的程序文件存放在哪里

#### find

find 起始路径 -name  “ ”

按文件大小查找文件

find 起始路径 -size +|-[KMG]

eg: find / -size -10k

#### grep

过滤文件内容

grep [-n] 关键字 文件路径

-n 可选表示在结果中匹配的行的行号

### wc

wc[-c -m -l -w] 文件路径 

-c: 统计bytes数量

-m ：统计字符数量

-l：统计行数

-w：统计单词数量

### 管道符

|  

|左边的结果作为右边的输入

### echo命令

在命令行内输出指定内容

echo 输出内容

### ``

反引号``

被其包围的字符会作为命令执行

### 重定向符

1. >\>将左边的内容覆盖到右边
   >
   >\>>将左边的内容追加到右边

### tail

 查看文件尾部的内容

tail [-f -num] linux路径

-f 表示持续跟踪

-num 查看尾部多少行 默认10行

### vi编辑器

vim为vi加强版

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-16%20111157.png)

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-16%20112853.png)
![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-16%20112824.png)

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-16%20123324.png)

## 用户和权限

### root用户

拥有最大操作权限 为root用户 

普通用户在home目录是不受限制的

su [-] 用户名

- 可选的 表示切换用户后加载环境变量

可以通过exit命令退回上一个用户 快捷键ctrl+d

sudo命令

为普通命令授权，临时以root身份认证

为普通用户配置sudo认证

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20173232.png)

### 用户 用户组

用户组管理

1. 创建用户组

groupadd 用户组名

2. 删除用户组名

groupdel 用户组名

用户

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20180837.png)

getent passwd 查看当前系统的目录

getent gruop                          用户组

### 权限

权限信息

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-19%20173929.png)

r:读权限

w：写

x:执行权限

### chmod

修改文件 文件夹的权限信息

chmod -R 权限 文件或文件夹

-R：对文件夹内全部的内容应用同样的操作

eg：chmod u=rwx，g=rx，o=x hello.txt

只有文件文件夹的所属用户或root用户可修改

最好还是根据rwx顺序写权限

\- - - :0

\- - x:1

\- w -:2

\- w x：3

### chown

修改文件文件夹的所属用户用户组

普通用户无法修改所属为其他用户或组

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-20%20104757.png)

## 快捷键

1. ctrl+c强制停止

2. ctrl+d退出/登出

3. history 查看历史输入过的命令

4. ！命令前缀 执行上次匹配前缀的命令
4. ctrl+r 输入内容去匹配历史命令 回车直接执行

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-20%20110751.png)

ctrl+l清屏

## 软件安装

### yum命令

RPM软件管理器 用于自动化安装Linux软件

yum [-y] [install| remove|search] 软件名称

-y自动确认 无需手动确认安装或卸载过程

需要root权限 或打开sudo权限

### systemctl

来控制 启动。停止，开机自启

能够被systemctl管理的软件 称为：服务

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-21%20204734.png)

### 软链接

在系统中创建软链接 可以将文件，文件夹链接到其他地方

类似与Windows的快捷方式

ln [-s] 参数1（被链接的） 参数2(目的地)

## 日期和时区

date [-d] [+格式化字符串]

-d: 按照给定的字符串显示日期 一般用于日期计算

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-22%20100557.png)

日期加减：

date -d “+1 day” 

修改时区

可以自动联网同步 也可以用ntpdate -u ntp.aliyun.com

## ip地址 主机名

对外联络的地址 

a.b.c.d 均为0到255

ifconfig 查看IP地址

127.0.0.1本机地址

0.0.0.0可以用来指代本机

在端口绑定中确认绑定关系

表示所有IP的意思表示任意IP访问

### 主 机名

hostname 查看主机名、

hostnamectl set -hostname 主机名

### 域名解析

IP地址的映射

先看本机的记录

Windows：C:\Windows\System32\drivers\etc\host

linux:/etc/hosts

DNS服务器114.114.114.114

## 网络请求

### ping

检查指定的网络服务器是否是可联通状态

ping [-c num] ip或主机名

-c检查的次数 不使用将无线次数检查

ping -c 3 39.156.66.10

### wget

非交互式文件下载器 可以在命令行里下载网络文件

wget -b url

-b后台下载 写日志

### curl

发起网路请求获取数据

或者下载

eg: curl cip.cc 

curl [-O] url

-O可以直接下载文件

### 端口

虚拟端口 IP地址只能锁定计算机，但无法锁定具体的程序

端口锁定程序 程序之间进行沟通

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-27%20114344.png)

### nmap netstat命令

nmap IP地址 查看对外暴露情况

查看端口占用情况

netstat -anp | grep 端口号，

查看指定端口占用情况

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-27%20124716.png)

### 进程管理

程序运行在操作系统中。是被操作系统所管理的

为管理运行的程序 每一个程序在运行时 被操作系统注册为一个进程

每个进程分配一个独有的进程ID

windows crl+shift+esc

linux  ps[-e -f]

-e 显示全部进程

-f 格式化显示

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-28%20151927.png)

常配合grep -n | 使用

关闭进程

语法 kill [-9] 进程ID

-9 表示强制关闭进程 不加看进程自我机制

### 主机占用情况

top查看cpu 内存等使用情况

类似与任务管理器

top - 15:38:02 up 32 min,  4 users,  load average: 0.57, 0.43, 0.27
Tasks: 171 total,   1 running, 170 sleeping,   0 stopped,   0 zombie
%Cpu(s):  6.0 us,  8.0 sy,  0.0 ni, 85.7 id,  0.0 wa,  0.0 hi,  0.3 si,  0.0 st
KiB Mem :   995676 total,   193584 free,   465652 used,   336440 buff/cache
KiB Swap:  2098172 total,  2098172 free,        0 used.   375380 avail Mem 

| 字段                             | 含义解释                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| `15:36:28`                       | 当前系统时间                                                 |
| `up 30 min`                      | 系统已持续运行 30 分钟（无重启记录）                         |
| `4 users`                        | 当前有 4 个用户登录系统（可能是本地终端、远程 SSH 连接等）   |
| `load average: 0.53, 0.40, 0.25` | 系统负载平均值：- 前 1 分钟：0.53- 前 5 分钟：0.40- 前 15 分钟：0.25**解读**：负载远低于系统 CPU 核心数（通常负载 < CPU 核心数为正常），系统压力极低，无卡顿风险。 |

| 字段           | 含义解释                                                     |
| -------------- | ------------------------------------------------------------ |
| `171 total`    | 系统当前总进程数：171 个（包含所有状态的进程）               |
| `2 running`    | 正在 CPU 上运行的进程数：2 个（表示当前有 2 个进程在主动占用 CPU 资源） |
| `169 sleeping` | 休眠进程数：169 个（进程等待资源（如 IO、信号），暂不占用 CPU，正常状态） |
| `0 stopped`    | 停止状态的进程数：0 个（无进程被手动暂停或信号停止）         |
| `0 zombie`     | 僵尸进程数：0 个（无 “僵尸进程”（进程已结束但父进程未回收资源），系统无资源泄漏风险 |

| 字段      | 含义解释                                                     |
| --------- | ------------------------------------------------------------ |
| `4.7 us`  | 用户空间 CPU 使用率：4.7%（应用程序（如浏览器、编辑器）占用的 CPU 资源） |
| `8.4 sy`  | 内核空间 CPU 使用率：8.4%（系统内核（如进程调度、内存管理）占用的 CPU 资源，略高但属正常） |
| `0.0 ni`  | 高优先级进程使用率：0%（无通过 `nice` 命令调整过优先级的进程在运行） |
| `86.6 id` | CPU 空闲率：86.6%（**核心指标**，空闲率极高，CPU 资源非常充足，无过载风险） |
| `0.0 wa`  | IO 等待 CPU 使用率：0%（无进程因等待磁盘 / 网络 IO 而阻塞 CPU，IO 性能正常） |
| `0.0 hi`  | 硬中断 CPU 使用率：0%（无硬件设备（如键盘、网卡）触发高优先级中断，硬件稳定） |
| `0.3 si`  | 软中断 CPU 使用率：0.3%（内核处理软件中断（如网络数据包）的开销，极低） |
| `0.0 st`  | 虚拟化窃取 CPU 率：0%（若为虚拟机，无宿主机 “窃取” 本虚拟机的 CPU 资源） |

| 字段                | 含义解释                                                     |
| ------------------- | ------------------------------------------------------------ |
| `995676 total`      | 物理内存总大小：约 972MB（1KiB=1024B，995676 / 1024 ≈ 972MB） |
| `193896 free`       | 完全空闲的物理内存：约 189MB（未被任何进程或缓存使用）       |
| `465644 used`       | 已使用的物理内存：约 455MB（包含应用程序占用、内核占用）     |
| `336136 buff/cache` | 缓存 / 缓冲内存：约 328MB（- `buffer`：用于临时存储磁盘 IO 数据；- `cache`：用于缓存已读取的文件内容；**关键**：这部分内存可被 “回收”（当应用需要内存时，系统会释放缓存给应用），并非 “真正占用”） |

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-28%20154233.png)

top有交互式选项

磁盘占用情况

df [-h]

网络状态监控

sar -n DEV num1 num2

num1 刷新间隔

num2 刷新次数

### 环境变量

env查看

环境变量是一种键值对

$符 用于取value值

#### 自行设置环境变量

1. 临时设置 export 变量名=变量值
1. 永久生效

- 针对当前用户生效 配置在当前用户

~/.bashrc文件中

- 针对所有用户生效 配置 /etc/profile

source 配置文件

  ## 文件上传下载

rz下载 sz删除

### 压缩和解压

.tar归档文件 将文件组装到一个.tar文件

.gz常见为.tar.gz.gzip格式压缩文件 可以减少压缩体积

语法tar [-c -v -x -f -z -C]参数

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-29%20105659.png)

压缩tar文件 -cvf

压缩gzip -zcvf

解压：

tar -xvf test.tar -C /home/itwu

zip命令压缩文件

zip [-r] 参数1 参数2

-r包含文件夹

解压 unzip [-d] 参数

## ubuntu

### man帮助页面

man man help

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-04%20151824.png)

### 用户权限操作

1. 添加用户adduser 用户名
1. passwd 用户名 改密码
1. id 用户名 查看指定用户
1. userdel
