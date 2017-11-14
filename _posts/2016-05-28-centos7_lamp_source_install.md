---
layout: post
title:  "centos7 lamp source install"
date:   2016-05-28 14:13:36 +0800
categories: lamp 
---

#LAMP compile

> date:2015/08/19 12:50:53

> date:2015/12/18 10:00:00

## apache

    sudo ln -s /usr/local/services/httpd-2.4.12 /usr/local/services/httpd

## mysql

    tar zxf mysql-5.6.26.tar.gz

    cd mysql-5.6.26

    make \
    -DCMAKE_INSTALL_PREFIX:PATH=/usr/local/services/mysql-5.6.26 \
    -DEXTRA_CHARSETS=all \
    -DENABLED_LOCAL_INFILE=1 \
    -DWITH_READLINE=1 \
    -DMYSQL_USER=mysql \
    -DENABLED_LOCAL_INFILE=1 \
    -DWITH_SSL=yes

    make

    make install

    sudo ln -s /usr/local/services/mysql-5.6.26 /usr/local/services/mysql

## php

### configure

    ./configure \
    --prefix=/usr/local/services/php-5.6.16 \
    --with-mysql=/usr/local/services/mysql \
    --with-mysqli=/usr/local/services/mysql/bin/mysql_config \
    --with-pdo-mysql=/usr/local/services/mysql \
    --with-apxs2=/usr/local/services/httpd/bin/apxs \
    --with-libxml-dir=/usr/local/services/libxml2 \
    --with-freetype-dir=/usr/local/services/freetype \
    --with-png-dir=/usr/local/services/libpng \
    --with-jpeg-dir=/usr/local/services/jpeg \
    --with-zlib-dir=/usr/local/services/zlib \
    --with-curl=/usr/local/services/curl \
    --with-gd=/usr/local/services/libgd \
    --with-openssl=/usr/local/services/openssl \
    --with-mhash=/usr/local/services/mhash \
    --with-mcrypt=/usr/local/services/libmcrypt \
    --enable-mbstring \
    --enable-mbregex \
    --enable-maintainer-zts \
    --enable-sockets \
    --enable-pcntl \
    --enable-sigchild \
    --enable-sysvmsg \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-soap \
    --enable-shmop \
    --enable-bcmath \
    --enable-zip \
    --enable-calendar \
    --enable-ctype \
    --enable-dom \
    --enable-filter \
    --enable-gd-native-ttf \
    --enable-hash \
    --enable-json \
    --enable-posix \
    --enable-shared \
    --enable-simplexml \
    --enable-static \
    --enable-tokenizer \
    --enable-xml \
    --enable-xmlwriter \
    --enable-pdo \
    --enable-inline-optimization \
    --enable-mysqlnd \
    --enable-exif \
    --enable-phar \
    --enable-cli \
    --enable-zend-signals \
    --enable-opcache

compile

    make

install

    make install


question


create symbol link

    sudo ln -s /usr/local/services/php-5.6.16 /usr/local/php

add env variable

    sudo echo "export PATH=$PATH:/usr/local/php" >> /etc/profile
    source /etc/profile

config php

    # /usr/local/services/php-5.6.16/lib/php/extensions/no-debug-zts-20131226/
    zend_extension=opcache.so

    apc
    pc cache 3.1.13 在2012年9月3日后就不再更新
    从php-5.5开始使用内置的 opcache

    # need dependence package, all of it will not build into php core
    sudo yum install libXpm libXpm-devel
    sudo yum install icu libicu libicu-devel

##notice

    php 5.5 need >= gd-2.1.0 

    complile gd
    ./configure \
    --prefix=/usr/local/services/gd-2.1.0 \
    --with-freetype=/usr/local/services/freetype \
    --with-png=/usr/local/services/libpng \
    --with-jpeg=/usr/local/services/jpeg


    ./configure --prefix=/usr/local/services/libmcrypt-2.5.8

    ./configure --prefix=/usr/local/services/mhash-0.9.9.9


     遗留问题
     --with-xpm-dir \    依赖于x11	
     --enable-intl \		国际化
     --with-config-file-scan-dir=/usr/local/php/conf \	貌似不生效


    1. 对所有包的依赖都按照软链接来建立,不要将具体的版本编译到内核中去。
    2. Error, X11/Xpm.h not found， 依赖X11, 不要将其包含在编译中, 方法： ./configure 后， vi main/php_config.h 文件中的 `#define HAVE_GD_XPM 1` 注释掉。https://bugs.php.net/bug.php?id=66204


