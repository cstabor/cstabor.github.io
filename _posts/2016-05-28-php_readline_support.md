---
layout: post
title:  "php readline support"
date:   2016-05-28 22:34:36 +0800
categories: php
tags: [php, php_ext]
---

## php-7.0.6 readline

./configure --with-php-config=/usr/local/services/php-7.0.6/bin/php-config

```
[user_00@dev201 readline]$ ldd modules/readline.so 
linux-vdso.so.1 =>  (0x00007fff0b9db000)
libedit.so.0 => /lib64/libedit.so.0 (0x00007facbdf09000)
libncurses.so.5 => /lib64/libncurses.so.5 (0x00007facbdce2000)
libtinfo.so.5 => /lib64/libtinfo.so.5 (0x00007facbdab7000)
libc.so.6 => /lib64/libc.so.6 (0x00007facbd6f6000)
libdl.so.2 => /lib64/libdl.so.2 (0x00007facbd4f2000)
/lib64/ld-linux-x86-64.so.2 (0x00007facbe364000)
```

--with-libedit

## php-5.6.16
readline/readline.h  No such file or directory

yum install readline readline-devel

```
[user_00@dev201 readline]$ ldd modules/readline.so
linux-vdso.so.1 =>  (0x00007fff3d358000)
libedit.so.0 => /lib64/libedit.so.0 (0x00007f6863050000)
libncurses.so.5 => /lib64/libncurses.so.5 (0x00007f6862e29000)
libtinfo.so.5 => /lib64/libtinfo.so.5 (0x00007f6862bfe000)
libc.so.6 => /lib64/libc.so.6 (0x00007f686283d000)
libdl.so.2 => /lib64/libdl.so.2 (0x00007f6862639000)
/lib64/ld-linux-x86-64.so.2 (0x00007f68634ab000)
```

after make
```
Libraries have been installed in:
/usr/local/src/php-5.6.16/ext/readline/modules

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the `-LLIBDIR`
flag during linking and do at least one of the following:
- add LIBDIR to the `LD_LIBRARY_PATH` environment variable
during execution
- add LIBDIR to the `LD_RUN_PATH` environment variable
during linking
- use the `-Wl,--rpath -Wl,LIBDIR` linker flag
- have your system administrator add LIBDIR to `/etc/ld.so.conf

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
```

error

```
[user_00@dev201 readline]$ php -a
Interactive mode enabled

php > echo 1;
php: symbol lookup error: /usr/local/services/php/extensions/readline.so: undefined symbol: append_history
```
