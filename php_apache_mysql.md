LAMP 环境编译

date:2015/8/19 12:50:53 

## apache ##


## mysql ##

软链接

	ln -s /usr/local/services/mysql-5.6.24 /usr/local/mysql

### php ###

	编译php

	./configure \
	--prefix=/usr/local/services/php-5.5.29 \
	--with-mysql=/usr/local/mysql \
	--with-mysqli=/usr/local/mysql/bin/mysql_config \
	--with-pdo-mysql=/usr/local/mysql \
	--with-apxs2=/usr/local/apache/bin/apxs \
	--with-libxml-dir=/usr/local/services/libxml2 \
	--with-gd=/usr/local/services/gd \
	--with-freetype-dir=/usr/local/services/freetype \
	--with-png-dir=/usr/local/services/libpng \
	--with-jpeg-dir=/usr/local/services/jpeg \
	--with-zlib-dir=/usr/local/services/zlib \
	--enable-mbstring \
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
	--enable-intl

php 5.5 need >= gd-2.1.0 

https://github.com/libgd/libgd/archive/gd-2.1.1.tar.gz


./configure \
--prefix=/usr/local/services/gd-2.1.1 \
--with-freetype=/usr/local/services/freetype \
--with-png=/usr/local/services/libpng \
--with-jpeg=/usr/local/services/jpeg
