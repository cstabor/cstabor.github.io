---
layout: post
title:  "shell flow control"
date:   2016-06-16 12:00:36 +0800
categories: linux
---

## if

```bash
#!/bin/bash

age=5

if [ 5 -lt $age ]
then
        out="age low than 1"
elif [ 5 -eq $age ]
then
        out="age eq 5"
else
        out="age greate than 5"
fi

echo $out
```
注意

> shell可以按照分号分割,也可以按照换行符分割
> 如果想一行写入多个命令，可以通过`;`分割

```bash
[user_00@node7 shell]$ a=2;if [[ a -gt 4 ]] ;then echo 'gt';else echo "not gt";fi;                        
not gt
[user_00@node7 shell]$ a=2;if [[ $a -gt 4 ]] ;then echo 'gt';else echo "not gt";fi;                        
not gt
```

## while

```bash
#!/bin/bash
i=10
while [[ $i -gt 5 ]]
do
        echo $i
        ((i--))
done
```

### while read
```bash
#!/bin/sh

while read line
do
	echo $line
done < /etc/hosts
```

## until

注意

> 直到满足条件退出，否则执行action。

```bash
#!/bin/sh

a=5
until [[ $a -lt 0 ]]
do
	echo $a
	((a--))
done
```

## switch

```sh
#!/bin/sh 

case $1 in
	start|begin)
		echo "start something"  
		;;
	stop|end)
		echo "stop something"  
		;;
	*)
		echo "ignore"  
		;;
esac
```

注意

> pattern 支持正则表达式,可以用下面字符：

```
*       任意字串
?       任意字元
[abc]   a, b, 或c三字元其中之一
[a-n]   从a到n的任一字元
|       多重选择
```

## select
```bash
#!/bin/sh 

select ch in "begin" "end" "exit"
do
	case $ch in
		"begin")
			echo "start something"  
			;;
		"end")
			echo "stop something"  
			;;
		"exit")
			echo "exit"  
			break
			;;
		*)
			echo "Ignorant"  
			;;
	esac
done
```

run result

```
[user_00@node7 syntax]$ sh select.sh 
1) begin
2) end
3) exit
#? 1
start something
#? 2
stop something
#? aa 
Ignorant
#? 3
exit

```
