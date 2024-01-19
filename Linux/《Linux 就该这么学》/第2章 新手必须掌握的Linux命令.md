# 第2章 新手必须掌握的Linux命令

## 2.1 shell

- shell 是终端程序的统称
- shell与bash的关系是包含与被包含的关系:教师这个职业,有许多相关从业者,其中bash就是优秀教师之一,被众多Linux发行版默认采用

## 2.2 命令相关知识

- Linux命令中 将可选参数使用 中括号引起来: man[命令参数]
- Linux命令参数分 长短格式:
  - 长格式: man --help
  - 短格式: man -h
- 常用组合键:
  - `Tab` :bash解释器中补全
  - `Ctrl+C` : 终止当前进程的运行
  - `Ctrl+L` : 清空当前终端内容(等价于清屏)

## 2.3 常用系统命令

1. echo :终端输出字符

2. date[+pattern] :显示or设置系统日期时间

> 按格式打印
>
> date "+%Y %m %d %H:%M:%S"
> 2024 01 16 21:41:13
>
> ***
>
> 设置时间为指定
>
> date -s "20201101 8:30:00"
>
> Sun Nov 1 08:30:00 CST 2020

3. timedatectl :设置系统时间

> #查看系统时间与时区的方法
>
> timedatectl status
>
> #设置系统日期 or时间
>
> timedatectl  set-time 2021-05-18
>
> timedatectl  set-time 9:30

4. reboot / poweroff :重启 / 关机
5. wget[参数] 网址 :获取网络文件

> -b 后台下载
>
> -P 下载到指定目录
>
> -p 下载所有资源

6. ==ps== : 进程状态查看 ,ps可以允许参数不加减号 

> -a 所有进程
>
> -u 用户以及详细作用
>
> -x 显示没有控制终端的进程
>
> ps aux 
>
> R(运行) S(中断) D(不可中断) Z(僵死) T(停止)

7. pstree
8. ==top== : 动态监控系统

9. nice :调整进程优先级
10. pidof[参数] 服务名 :查询进程pid

11. kill[参数] 进程pid : 终止指定pid的进程
12. killall [参数] 服务名称 : 终止指定服务的全部进程

## 2.4 系统状态检测命令

1. ifconfig :查看网络与网卡 interface config
2. uname [-a]:查看系统内核架构 unix name

3. uptime :查看系统负载 ,1/5/15 平均负载压力,建议负载值 1 左右,生产环境不要超过5即可
4. ==free[-h]== :查看系统内存使用情况

5. who :当前登录主机的用户终端信息

6. last : 显示主机登录访问信息

7. ping[参数] 地址 :测试网络连通性

> -c 总发送次数
>
> -W 最长等待时间
>
> ping -c 4 baidu.com

8. tracepath[参数] 域名 :显示数据包到达目的主机中经过所有路由信息
9. ==netstat[参数]== : 显示网络相关信息

> -a 显示所有连接中 socket
>
> -p 显示正在使用的socket
>
> -t 显示 tcp协议
>
> -u 显示udp协议

10. history[-c] : 显示历史命令 , `!编码数字` 执行history指定命令

> -c 清空所有历史记录(默认1k条)

11. sosreporte : 收集系统信息输出诊断文档 

## 2.5 查找定位文件命令

1. pwd : 显示用户当前工作目录,print working directory
2. cd\[参数]\[目录] :切换路径

> #切换上一次所处的目录
>
> cd - 
>
> #切回家目录
>
> cd ~

3. ls[参数]\[文件名称] :显示目录文件信息

> -a 显示全部
>
> -l 查看文件元数据

4. tree : 树结构查看当前目录内容

5. ==find[查找范围] 条件== :查找文件所在的位置

> -name
>
> -user
>
> -group
>
> -mtime -n +n 匹配修改时间(-n n天以内,+n n天以前)
>
> -atime -n +n 匹配访问文件的时间
>
> -cmtime -n +n 匹配修改文件权限的时间
>
> -size
>
> --type
>
> -exec ... {} \\;
>
> #删除指定目录下2天以前的所有日志文件
>
> find /your/path -name *.log -exec rm -f {} \\;

6. whereis 命令名称: 查找二进制程序位置

7. which 命令名称:按照指定名称快速搜索二进制程序（命令）所对应的位置

## 2.6 文本文件编辑命令

1. cat[参数] 文件 :查看较少的纯文本文件

> #-n显示行号
>
> cat -n xx.log

2. more[参数] 文件 :查看纯文本文件（内容较多的）,使用空格键或回车键向下翻页

3. head [参数] 文件 /tail [参数] 文件: 查看纯文本文件的前N行/后N行

> head -n 10 xx.log
>
> #-f 持续刷新一个文件的内容
>
> tail -f xx.log 

4. tr :tr命令用于替换文本内容中的字符，英文全称为“translate”，语法格式为“tr [原始字符] [目标字符]

5. wc :wc命令用于统计文本的行数、字数、字节数

> wc /etc/passwd
>
>  17  34 871 /etc/passwd
>
> 从左至右:行数 字数 字节数
>
> -l 仅显示行数
>
> -w 仅显示字数
>
> -c 仅显示字节数

6. ==stat== :stat命令用于查看文件的具体存储细节和时间等信息，英文全称为“status”，语法格式为“stat文件名称

> Linux文件有三种时间:
>
> - access time 最后访问时间(Atime)
> - modify time 内容最后一次修改时间(Mtime)
> - chang time  属性最后一次修改时间(Ctime)

7.==grep==:grep命令用于按行提取文本内容，语法格式为“grep [参数]文件名称”。

> -n 显示行号
>
> -v 反选
>
> #查找当前系统不允许登录系统的所有用户
>
> grep /sbin/nologin /etc/passwd

8. cut:按“列”提取文本内容，语法格式为“cut [参数]文件名称

9. diff :diff命令用于比较多个文件之间内容的差异，英文全称为“different”，语法格式为“diff [参数]文件名称A文件名称B”。
10. uniq :uniq命令用于去除文本中连续的重复行，英文全称为“unique”，语法格式为“uniq [参数]文件名称”
11. sort :sort命令用于对文本内容进行再排序，语法格式为“sort [参数]文件名称"

## 2.7 文件目录管理命令

1. touch :创建空白文件 or设置文件时间

> -a 仅修改Atime
>
> -m 仅修改Mtime
>
> -d 同时修改Atime与Mtime

2. mkdir
3. cp

> -p 保留原始文件属性
>
> -d 若对象为“链接文件”，则保留该“链接文件”的属性
>
> -r 递归复制目录
>
> -a 等价-pdr
>
> -i 若目标文件存在则询问是否覆

4. mv

5. rm
6. dd :dd命令用于按照指定大小和个数的数据块来复制文件或转换文件，语法格式为“dd  if=参数值of=参数值count=参数值bs=参数值
7. file : file命令用于查看文件的类型，语法格式为“file文件名称”

8. tar : 压缩or解压 ,-f参数特别重要，它必须放到参数的最后一位，代表要压缩或解压的软件包名称

> -C 指定解压目录
>
> #用gzip解压,显示过程
>
> tar -xzvf xx.tar.gz -C ~
>
> #压缩
>
> tar -czvf 打包文件