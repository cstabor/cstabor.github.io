---
layout: post
title: "php apache mysql"
date: 2015-08-19 11:00:00 +0800 
categories: php 
tag: php mysql httpd LAMP 
---
* content
{:toc}

#LAMP source compile

> date:2015/08/19 12:50:53

> date:2015/12/18 10:00:00

## apache

    sudo ln -s /usr/local/services/httpd-2.4.12 /usr/local/apache

## mysql

    sudo ln -s /usr/local/services/mysql-5.6.24 /usr/local/mysql

## php

configure

    ./configure \
    --prefix=/usr/local/services/php-5.6.16 \
    --with-config-file-path=/usr/local/php/lib \
    --with-config-file-scan-dir=/usr/local/php/conf \
    --with-pdo-mysql=/usr/local/mysql \
    --with-apxs2=/usr/local/apache/bin/apxs \
    --with-libxml-dir=/usr/local/services/libxml2 \
    --with-freetype-dir=/usr/local/services/freetype \
    --with-png-dir=/usr/local/services/libpng \
    --with-jpeg-dir=/usr/local/services/jpeg \
    --with-zlib-dir=/usr/local/services/zlib \
    --with-curl=/usr/local/services/curl \
    --with-gd=/usr/local/services/gd \
    --with-openssl \
    --with-xpm-dir \
    --with-mhash \
    --enable-mbstring \
    --enable-mbregex \
    --enable-maintainer-zts \
    --enable-sockets \
    --enable-pcntl \
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
    --enable-intl \
    --enable-phar \
    --enable-cli \
    --enable-opcache

compile

    make

install

    make install

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

    # need dependence package
    sudo yum install libXpm libXpm-devel
    sudo yum install icu libicu libicu-devel

##notice

    php 5.5 need >= gd-2.1.0 

    https://github.com/libgd/libgd/archive/gd-2.1.1.tar.gz

    complile gd
    ./configure \
    --prefix=/usr/local/services/gd-2.1.1 \
    --with-freetype=/usr/local/services/freetype \
    --with-png=/usr/local/services/libpng \
    --with-jpeg=/usr/local/services/jpeg
