---
layout: post
title:  "vim encoding"
date:   2016-05-28 14:13:36 +0800
categories: vim
---

## cp936 VS gb2312
cp936是微软自己发布的用在文件系统中的编码方式。而bg2312是中国国家标准。
```
mount -o iocharset=cp936
比
mount -o iocharset=gb2312 
支持中文支持的好
```

## enca 检测文件编码
```
yum install -y enca
```

file filename 检测文件的编码不一定准确

```
enca filename

enca: Cannot determine (or understand) your language preferences.
Please use `-L language', or `-L none' if your language is not supported
(only a few multibyte encodings can be recognized then).
Run `enca --list languages' to get a list of supported languages.
```

```
$ enca -L zh filename
Simplified Chinese National Standard; GB2312
```
```
[user_00@thinkpad db_init_20160111]$ enca -L zh readme.txt 
Simplified Chinese National Standard; GB2312

[user_00@thinkpad db_init_20160111]$ enca --list language
belarusian: CP1251 IBM866 ISO-8859-5 KOI8-UNI maccyr IBM855 KOI8-U
bulgarian: CP1251 ISO-8859-5 IBM855 maccyr ECMA-113
czech: ISO-8859-2 CP1250 IBM852 KEYBCS2 macce KOI-8_CS_2 CORK
estonian: ISO-8859-4 CP1257 IBM775 ISO-8859-13 macce baltic
croatian: CP1250 ISO-8859-2 IBM852 macce CORK
hungarian: ISO-8859-2 CP1250 IBM852 macce CORK
lithuanian: CP1257 ISO-8859-4 IBM775 ISO-8859-13 macce baltic
latvian: CP1257 ISO-8859-4 IBM775 ISO-8859-13 macce baltic
polish: ISO-8859-2 CP1250 IBM852 macce ISO-8859-13 ISO-8859-16 baltic CORK
russian: KOI8-R CP1251 ISO-8859-5 IBM866 maccyr
slovak: CP1250 ISO-8859-2 IBM852 KEYBCS2 macce KOI-8_CS_2 CORK
slovene: ISO-8859-2 CP1250 IBM852 macce CORK
ukrainian: CP1251 IBM855 ISO-8859-5 CP1125 KOI8-U maccyr
chinese: GBK BIG5 HZ
none:

[user_00@thinkpad db_init_20160111]$ enca -L chinese readme.txt 
Simplified Chinese National Standard; GB2312

```


vim 中设置
vim ~/.vimrc
```
set fileencodings=utf-8,cp936
```
当设置完上面之后，当用户在使用vim打开文件的时候，
vim 依次侦测文件编码是否属于fileencodings 中列的文件编码
如果属于，则采用相应的编码读取文件;反之，文件将被解析成乱码。

当文件被某一种编码识别之后。在vim 中使用set 将展示已经侦测的文件编码
```
fileencoding=cp936
```
