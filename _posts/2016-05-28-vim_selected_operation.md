---
layout: post
title:  "vim selected operation"
date:   2016-05-28 18:23:36 +0800
categories: vim 
---

快速对引号或括号等标点内的内容进行选中、删除、复制操作

```
ci’、ci”、ci(、ci[、ci{、ci<		 	更改配对标点符号中的文本
di’、di”、di(或dib、di[、di{或diB、di< 	删除配对标点符号中的文本
yi’、yi”、yi(、yi[、yi{、yi< 		 	复制配对标点符号中的文本
vi’、vi”、vi(、vi[、vi{、vi< 		 	选中配对标点符号中的文本
```

另外，若将`i`变成`a`可以连配对标点也一起操作

示例

```
111"222"333
```

将光标移到"222"的任何一个字符处

输入命令`di"` ,文本会变成： 111""333

输入命令`da"` ,文本会变成： 111333

reference

> http://www.linuxsong.org/2010/09/vim-quick-select-copy-delete/
