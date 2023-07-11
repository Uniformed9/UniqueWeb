# linux基本概念和命令
---
###命令行操作
####find命令
find ***[路径]*** ***[选项]*** ***[操作]***  
选项    |  含义
------  | ------
-name |根据文件名查找
-perm |根据文件权限查找
例子<span>`find . -name "*.c"`</span>  
####mv命令
mv ***[options]***  ***from*** ***to***

----
###权限
####chmod命令
chmod ***[参数]*** ***[数字权限]*** ***[文件]***  
<span style="">`chmod u+x,g-x,o=rw test.c`</span>  
<span style="">`chmod 777 test.c`</span>

####chown命令
只有root才能更改文件的所有权
chown ***[参数]*** ***[数字权限]*** ***[文件]*** 
<span style="">`chown root:root ./test.c`</span> 

####隐藏权限
&emsp;&emsp;使用<span>`lsattr`</span>查看隐藏权限返回<span>`-----a--------e------- ./test.c`</span>，其中e代表设置了扩展属性，a仅允许追加内容，而不允许覆盖和删除原有的内容，日志文件常用。  
&emsp;&emsp;使用<span>`chattr +a target`</span>增加权限<span>`chattr -a target`</span>删减权限

####访问控制列表
针对某一用户进行特别的控制的时候，可以使用访问控制列表  
~~查看命令~~<span>`getfacl test.c`</span>  
~~设置命令~~<span>`setfacl -m u:aaa:rwx test.c`</span>  
#####setfacl [选项] [用户] [权限] [文件]
-m表示文件  
-R表示递归，对目录使用  
-b表示删除访问控制列表例如<span>`getfacl -m u:aaa:rwx test.c`</span>  
aaa是用户  
test.c是文件

####提权
在不切换成超级用户的情况下，执行超级用户的命令(sudo)  

###进程
进程（process）是指正在执行的程序的实例。每个进程都是一个独立的执行单元，具有自己的代码、数据、内存空间和系统资源，包括CPU时间、文件描述符、网络连接等。
####操作进程的命令
```ps -aux```用于显示跟踪cpu占用率和内存占用率   
```ps -ef```用于跟踪父进程和完整的启动命令
```
#找出消耗内存最多的前10名进程
ps -aux --sort -pcpu | head -10  
#分页查看进程
ps -aux |more
#按照cpu占用来排序并且分页显示
ps -aux --sort -pcpu|less -N  
# -o指定要输出的信息列
ps -o pid,ppid,pgrp,session,tpgid,comm
```

```top```命令分析进程占用的资源  

```top -p 1 #显示指定进程信息 kill 123 #中止特定进程 killall和pkill 都是根据进程名来中止进程的```
###端口
端口是用于标识进程的逻辑地址，它是一个16位的数字（取值范围为0-65535），用于标识网络传输层协议（如TCP、UDP等）中的应用程序。端口是用于标识进程的逻辑地址，它是一个16位的数字（取值范围为0-65535），用于标识网络传输层协议（如TCP、UDP等）中的应用程序。
####查看端口
```#anp显示所有的TCP和UDP连接状态netstat -anp |gerp 80```