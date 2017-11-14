---
layout: post
title:  "byte order"
date:   2016-05-28 22:03:36 +0800
categories: linux
---
* content
{:toc}

# hexdump

$ cat a.txt

```
abc
```

示例

```
[user_00@thinkpad tmp]$ hexdump -x a.txt
0000000    6261    0a63                                               
0000004

[user_00@thinkpad tmp]$ hexdump a.txt
0000000 6261 0a63                              
0000004
```

实际的值

```
0000000 ba \nc                              
0000004
```

ascii 值

```
\n 10 换行（newline) `\x0a`
\r 13 回车 (return) `\x0d`
```
换行符

```
window  `\r\n`
linux `\n`

```

### 小端序little-endian
最低位字节0x0D存储在最低的内存地址处。后面字节依次存在后面的地址处。

### 大端序big-endian
最高位字节0x0A存储在最低的内存地址处。下一个字节0x0B存在后面的地址处。类似于十六进制字节从左到右的阅读顺序。

`x86`处理其一般都是`little-endian`

### 网络序
网络传输一般采用大端序，也被称为`网络字节序`，或`网络序`。IP协议中定义大端序为网络字节序。

### reference
1. [字节序](https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82%E5%BA%8F)
2. [hexdump](http://man.linuxde.net/hexdump)
3. [base64](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001399413803339f4bbda5c01fc479cbea98b1387390748000)
4. [wikipedia base64](https://zh.wikipedia.org/wiki/Base64)
5. [base64 blog](http://www.ruanyifeng.com/blog/2008/06/base64.html)
6. [base64 url](http://www.cnblogs.com/lifesting/archive/2012/07/12/2587923.html)
