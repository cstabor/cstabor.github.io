---
layout: post
title:  "Linux Process Tool"
date:   2017-11-08 17:00:00 +0800
categories: linux
tag: linux shell
---

* TOC
{:toc}

# 进程


## 1. strace

strace - trace system calls and signals



### 1.1 诊断进程ID

```
// strace a running process
strace -p [pid]

// strace a running process and threads
strace -fp [pid]

// strace a running process and print strings
strace -s 80 -fp [pid]
```

示例：

注意需要root权限

```
# strace -p 2061
strace: Process 2061 attached
semop(393224, [{0, -1, SEM_UNDO}], 1
```

### 1.2 诊断程序

```
// strace a program
strace ./program

// strace a program and threads
strace -f ./program

// strace a program and print strings
strace -s 80 -f ./program
```

### 1.2 统计汇总进程的调用

```
strace -c -p pid

strace -c process_name
```

示例

```
# strace -c -p 1191
strace: Process 1191 attached

^Cstrace: Process 1191 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 30.82    0.000777          22        35           open
 28.32    0.000714          20        35           read
 23.24    0.000586          17        35           epoll_wait
 17.61    0.000444          13        35           close
------ ----------- ----------- --------- --------- ----------------
100.00    0.002521                   140           total
```



### 1.3 按进程名查看

```
strace ls

strace ./hello
```



### 1.4 查看进程的线程

-f          Trace  child  processes  as  they  are  created  by currently traced processes as a result of the fork(2), vfork(2) and clone(2) system calls.  Note that -p PID -f will attach all threads of process PID if it is  multi-threaded,  not  only thread with thread_id = PID.

```
strace -f -p pid

strace -f proccess_name
```



### 1.5 时间统计

-r 表示相对时间

-T 表示绝对时间

简单统计可以用`-r`，但是需要注意的是在多任务背景下，CPU随时可能会被切换出去做别的事情，所以相对时间不一定准确，此时最好使用`-T`，在行尾可以看到操作时间，可以发现确实很慢。

```
$ strace -r ./hello
     0.000000 execve("./hello", ["./hello"], [/* 66 vars */]) = 0
     0.000417 brk(NULL)                 = 0x1765000
     0.000102 mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f7af22cd000
     0.000095 access("/etc/ld.so.preload", R_OK) = -1 ENOENT (No such file or directory)
     0.000079 open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
     0.000068 fstat(3, {st_mode=S_IFREG|0644, st_size=135921, ...}) = 0
     0.000070 mmap(NULL, 135921, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f7af22ab000
     0.000054 close(3)                  = 0

```



### 1.6 输出到标准输出

注意: strace的结果在标准错误里，使用前最好重定向到标准输出。

```
$ strace -T ./hello 2>&1 | grep -B 5 brk
execve("./hello", ["./hello"], [/* 66 vars */]) = 0 <0.000150>
brk(NULL)                               = 0xf35000 <0.000031>
```



### 1.7 输出到指定文件

-o filename Write  the trace output to the file filename rather than to stderr.

```
$ strace -o /tmp/strace.out -T ./hello
```



### 1.8 跟踪指定调用的耗时

```
       -e expr     A qualifying expression which modifies which events to trace or how to trace them.   The
                   format of the expression is:

                             [qualifier=][!]value1[,value2]...

                   where  qualifier is one of trace, abbrev, verbose, raw, signal, read, or write and value
                   is a qualifier-dependent symbol or number.  The default qualifier is  trace.   Using  an
                   exclamation  mark  negates  the  set  of  values.   For example, -e open means literally
                   -e trace=open which in turn means  trace  only  the  open  system  call.   By  contrast,
                   -e trace=!open  means  to trace every system call except open.  In addition, the special
                   values all and none have the obvious meanings.

```

示例

```
$ strace -e open -T ./hello
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3 <0.000015>
open("/lib64/libc.so.6", O_RDONLY|O_CLOEXEC) = 3 <0.000015>
file num: 256
+++ exited with 0 +++

```



### 1.9 内核态和用户态

如果用 strace 跟踪一个进程，输出结果很少，可以试试 ltrace，可能会发现别有洞天。记住有内核态和用户态之分。







### refer

1. https://blog.packagecloud.io/eng/2015/11/15/strace-cheat-sheet/

## 2. ltrace



ltrace - A library call tracer

```
strace
https://rainbow.chard.org/2011/10/02/debug-like-a-sysadmin/


ptrace - process trace
pidx

mtrace (3)           - malloc tracing
muntrace (3)         - malloc tracing
backtrace (3)        - support for application self-debugging
tcptraceroute (8)    - print the route packets trace to network host

/usr/bin/ltrace
/usr/bin/mtrace
/usr/bin/strace
/usr/bin/blktrace
/usr/bin/btrace
/usr/bin/dtrace
/usr/bin/xtrace

/usr/sbin/autrace

lstat("/home/data/services/yesdatphp/bosslite/api/runtime/logs/app.log", {st_mode=S_IFREG|0644, st_size=4269249, ...}) = 0
lstat("/home/data/services/yesdatphp/bosslite/api/runtime/logs", {st_mode=S_IFDIR|0775, st_size=4096, ...}) = 0
lstat("/home/data/services/yesdatphp/bosslite/api/runtime", {st_mode=S_IFLNK|0777, st_size=28, ...}) = 0
readlink("/home/data/services/yesdatphp/bosslite/api/runtime", "/data/logs/bosslite_api-1.0/", 4096) = 28
```



## 3. 进程查看

 

### 3.1 (pidof)按进程名查进程号

pidof -- find the process ID of a running program.

```shell
pidof process_name
```

示例

```
$ pidof httpd
2061 2060 2059 2058 2057 2056 2055 2054 2047 2046 2045 2044 1899 1898 1846 1711 1710 1709 1708 1707 1706 1705 1704 1703 1702 1615
```

### 3.2 (pgrep) 过滤最新进程ID

pgrep, pkill - look up or signal processes based on name and other attributes

示例

```
pgrep -n httpd
2061
```



### 3.3 (pwdx) 查看进程的路径

report current working directory of a process



示例

```
$ pwdx 1191
1191: /usr/local/services/redis-3.2.0/data/6379
```



### 3.4 (top) 查看系统负载

#### 3.4.1 间隔时间查看系统负载

每间隔一秒输出一次系统负载

```
top -d 1
```

也可以进入 `top` 命令后 输入 `d`  再输入 `1`，实现相同的功能



#### 3.4.2 查看CPU列表

进入 `top` 后 按 `1`

```
%Cpu0  :  1.2 us,  0.4 sy,  0.0 ni, 94.9 id,  3.5 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu1  :  0.8 us,  0.0 sy,  0.0 ni, 99.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu2  :  2.0 us,  0.4 sy,  0.0 ni, 97.6 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu3  :  1.2 us,  0.4 sy,  0.0 ni, 98.4 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu4  :  0.4 us,  0.4 sy,  0.0 ni, 99.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu5  :  0.8 us,  0.4 sy,  0.0 ni, 98.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
%Cpu7  :  0.8 us,  0.0 sy,  0.0 ni, 99.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st

```

#### 3.4.3 按CPU排序

`shift + P`

#### 3.4.4 查看指定进程ID的负载

```
top -p pid
```

示例

```
top -p 25837,2492
```

注意：分隔符是 逗号

#### 3.4.5 根据用户查看进程httpd负载

1. top 进入负载检测页面
2. 输入 `u`  再输入 apache 的运行用户 `nobdoy`  ，即展示了 httpd 的负载进程相关参数

```
top - 18:08:27 up 2 days,  8:35,  6 users,  load average: 0.25, 0.28, 0.22
Tasks: 379 total,   2 running, 377 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.5 us,  0.5 sy,  0.0 ni, 97.8 id,  0.2 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 12009984 total,   393028 free,  7572180 used,  4044776 buff/cache
KiB Swap:  6103036 total,  6103036 free,        0 used.  3228692 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                                 
15461 nobody    20   0  381412  36220   5752 S   0.0  0.3   0:09.40 httpd                                                   
15462 nobody    20   0  382224  36864   5824 S   0.0  0.3   0:09.61 httpd                                                   
15463 nobody    20   0  378092  36684   5656 S   0.0  0.3   0:08.26 httpd                                                   
15464 nobody    20   0  380728  35660   5760 S   0.0  0.3   0:08.61 httpd                                                   
15465 nobody    20   0  384556  39368   5752 S   0.0  0.3   0:09.59 httpd                                                   
15466 nobody    20   0  381716  36248   5712 S   0.0  0.3   0:08.37 httpd                                                   
15467 nobody    20   0  379208  34324   5956 S   0.0  0.3   0:07.99 httpd                                                   
15468 nobody    20   0  376740  36072   6032 S   0.0  0.3   0:07.93 httpd                                                   
15469 nobody    20   0  375224  34196   5676 S   0.0  0.3   0:06.31 httpd
```







### 3.5 (ps) 查询



#### 3.5.1 按名称查询

```
-C cmdlist
	Select by command name.  This selects the processes whose executable name is given in cmdlist.

h      
	No header.  (or, one header per screen in the BSD personality).  The h option is problematic.  Standard
	BSD ps uses this option to print a header on each page of output, but older Linux ps uses this option to
	totally disable the header.  This version of ps follows the Linux usage of not printing the header unless
  	the BSD personality has been selected, in which case it prints a header on each page of output.
  	Regardless of the current personality, you can use the long options --headers and --no-headers to enable
  	printing headers each page or disable headers entirely, respectively.

-o format
	User-defined format.  format is a single argument in the form of a blank-separated or comma-separated
	list, which offers a way to specify individual output columns. 
	stat, pid, ppid, cmd

```



示例1

```
$ ps -C httpd
  PID TTY          TIME CMD
15454 ?        00:00:03 httpd
15461 ?        00:00:09 httpd
15462 ?        00:00:09 httpd
15463 ?        00:00:08 httpd
15464 ?        00:00:08 httpd
15465 ?        00:00:09 httpd
15466 ?        00:00:08 httpd
15467 ?        00:00:07 httpd
```

示例2

```
[user_00@node7 yesdatphp]$ ps h -C httpd
15454 ?        Ss     0:03 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15461 ?        S      0:09 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15462 ?        S      0:09 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15463 ?        S      0:08 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15464 ?        S      0:08 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15465 ?        S      0:09 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15466 ?        S      0:08 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15467 ?        S      0:07 /usr/local/services/httpd-2.4.12/bin/httpd -k start
15468 ?        S      0:07 /usr/local/services/httpd-2.4.12/bin/httpd -k start
```

示例3

```
[user_00@node7 yesdatphp]$ ps h -ostat,pid -C httpd
Ss   15454
S    15461
S    15462
S    15463
S    15464
S    15465
S    15466
S    15467

```







# 子进程



## 1.1 (ps)子进程列表

```
ps -ostat,cmd --ppid <ppid>
```

--ppid   指定父进程ID

-o

​	stat    状态

​	pid     进程ID

​	cmd   启动命令

​	args   与 cmd 类似

​	lstart  启动时间



示例

```
[user_00@dev201 6379]$ ps -opid,stat,cmd --ppid 47466
  PID STAT CMD
48683 S    /usr/local/services/httpd-2.4.12/bin/httpd -k start
48684 S    /usr/local/services/httpd-2.4.12/bin/httpd -k start
48685 S    /usr/local/services/httpd-2.4.12/bin/httpd -k start
48686 S    /usr/local/services/httpd-2.4.12/bin/httpd -k start
```



## 1.2 (pstree)子进程列表



```
[user_00@node7 yesdatphp]$ pstree -p 15454
httpd(15454)─┬─httpd(15461)
             ├─httpd(15462)
             ├─httpd(15463)
             ├─httpd(15464)
             ├─httpd(15465)
             ├─httpd(15466)
             ├─httpd(15467)

```

### 1.2.1 查看指定用户的进程树

```
pstree <user_name>
```

示例

```
[user_00@node7 yesdatphp]$ pstree mysql
mysqld_safe───mysqld───18*[{mysqld}]

```



#线程

线程是现代操作系统上进行并行执行的一个流行的编程方面的抽象概念。当一个程序内有多个线程被叉分出用以执行多个流时，这些线程就会在它们之间共享 特定的资源（如，内存地址空间、打开的文件），以使叉分开销最小化，并避免大量高成本的IPC（进程间通信）通道。这些功能让线程在并发执行时成为一个高 效的机制。
在Linux中，程序中创建的线程（也称为轻量级进程，LWP）会具有和程序的PID相同的“线程组ID”。然后，各个线程会获得其自身的线程 ID（TID）。对于Linux内核调度器而言，线程不过是恰好共享特定资源的标准的进程而已。经典的命令行工具，如ps或top，都可以用来显示线程级 别的信息，只是默认情况下它们显示进程级别的信息。



## 1.1 (ps)查看

```
ps -T -p <pid>
```

-T  开启线程查看

示例：

```
[user_00@node7 apache-tomcat-8.5.23]$ ps -T -p 8488
  PID  SPID TTY          TIME CMD
 8488  8488 pts/1    00:00:00 java
 8488  8503 pts/1    00:00:00 java
 8488  8508 pts/1    00:00:00 java
 8488  8509 pts/1    00:00:00 java
 8488  8510 pts/1    00:00:00 java
 8488  8511 pts/1    00:00:00 java
 8488  8512 pts/1    00:00:00 java
 8488  8513 pts/1    00:00:00 java
```

SPID  表示线程ID

CMD  表示线程名称

## 1.2 (top)查看

```
top -H -p <pid>
```

-H   列出所有linux线程

示例：

```
top - 15:37:41 up 2 days,  6:04,  6 users,  load average: 0.38, 0.17, 0.14
Threads:  51 total,   0 running,  51 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.0 us,  0.5 sy,  0.0 ni, 97.4 id,  0.2 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 12009984 total,   210388 free,  7084520 used,  4715076 buff/cache
KiB Swap:  6103036 total,  6103036 free,        0 used.  3678600 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                       
 8555 user_00   20   0 6948056 145960  11668 S  0.3  1.2   0:00.13 java                                          
 8488 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.00 java                                          
 8503 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.76 java                                          
 8508 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.01 java                                          
 8509 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.01 java                                          
 8510 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.01 java                                          
 8511 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.00 java                                          
 8512 user_00   20   0 6948056 145960  11668 S  0.0  1.2   0:00.01 java 
```

也可以进入 top 之后再按 `H` ，显示线程

