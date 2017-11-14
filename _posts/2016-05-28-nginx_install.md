---
layout: post
title:  "nginx install"
date:   2016-05-28 14:13:36 +0800
categories: nginx
---

> 版本：nginx-1.8.1

> stable

## 下载解压
```
cd /usr/local/src
wget http://nginx.org/download/nginx-1.8.1.tar.gz
tar zxf nginx-1.8.1.tar.gz
cd nginx-1.8.1
```

## 编译选项

```
./configure --prefix=/usr/local/services/nginx-1.8.1 \
--with-http_ssl_module \
--with-pcre \
--user=www \
--group=www
```
