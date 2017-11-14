---
layout: post
title:  "centos7 software"
date:   2016-05-28 14:13:36 +0800
categories: centos 
---

### 环境初始化
```
yum install git
yum install gcc g++ gcc-c++
```

### 上传下载
```
yum install lrzsz
```

### google-chrome
```
vim /etc/yum.repos.d/google-chrome.repo
[google-chrome]
name=Google-x86_64
baseurl=http://dl.google.com/linux/rpm/stable/x86_64
enabled=1
gpgcheck=0
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub

yum install google-chrome-stable
```


### ntfs-3g
```
wget -O /etc/yum.repos.d/epel.repo     # 添加源 http://mirrors.aliyun.com/repo/epel-7.repo
yum update
yum install ntfs-3g

源：http://mirrors.aliyun.com/help/epel，说明里面没有写CentOS7的源，实际上是有的，把里面的5/6改成7就行了。
```
#### mount ntfs error
```
source: http://www.blogjava.net/freeman1984/archive/2013/05/17/399427.html
问题：
      # mount -t ntfs /dev/sdc1 /mnt/usb
      mount: unknown filesystem type ‘ntfs’
这是由于 上无法识别NTFS格式的分区。

解决办法：
      通过使用 ntfs-3g 来解决。
      打开ntfs-3g的下载点http://www.tuxera.com/community/ntfs-3g-download/ ，将最新稳定ntfs-3g-2011.1.13下载到linux，
执行以下命令安装ntfs-3g：
# tar zxvf  ntfs-3g-2011.1.13.tgz
# cd ntfs-3g-2011.1.15
#./configure
#make
#make install

mkdir /mnt/usb
mount -t ntfs-3g  /dev/sdc1 /mnt/usb
```

### shadowsocks qt5 客户端
```
cd /etc/yum.repos.d/
wget https://copr.fedoraproject.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
yum install shadowsocks-qt5
```
#### 安装过程遇到报错
```
Requires: libQt5Core.so.5()(64bit)

解决链接：
https://github.com/librehat/shadowsocks-qt5/issues/175
operation
cd /etc/yum.repos.d/
wget https://copr.fedoraproject.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
```

### shadowsocks python 客户端
```
sudo yum install python-pip python-dev build-essential python-m2crypto
sudo pip install shadowsocks
```

vim /home/user_00/bin/ss.sh
```
#!/bin/bash

serverIp='www.xyz.com'
serverPort='1234'
localIp='0.0.0.0'
localPort='1080'
password='123456'
method='rc4-md5'
sslocal -s $serverIp -p $serverPort -b $localIp -l $localPort -k $password -m $method
```
在后台启动
```
nohup /home/user_00/bin/ss.sh 2 >&1 /dev/null &
```
sslocal 帮助
```
[user_00@thinkpad workspace]$ sslocal help
ERROR: config not specified
usage: sslocal [OPTION]...
A fast tunnel proxy that helps you bypass firewalls.

You can supply configurations via either config file or command line arguments.

Proxy options:
  -c CONFIG              path to config file
  -s SERVER_ADDR         server address
  -p SERVER_PORT         server port, default: 8388
  -b LOCAL_ADDR          local binding address, default: 127.0.0.1
  -l LOCAL_PORT          local port, default: 1080
  -k PASSWORD            password
  -m METHOD              encryption method, default: aes-256-cfb
  -t TIMEOUT             timeout in seconds, default: 300
  --fast-open            use TCP_FASTOPEN, requires Linux 3.7+
```

#### proxyswithysharp

https://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt

### proxychain
```
git clone https://github.com/rofl0r/proxychains-ng
cd proxychains-ng/
configure
make
make install
make install-config

output：./tools/install.sh -D -m 644 src/proxychains.conf /usr/local/etc/proxychains.conf

vim /usr/local/etc/proxychains.conf
add the following text:
sockets5    127.0.0.1    1080

```

### flash
```
Flash插件主要是看在线视频的时候要用。Google浏览器自带了Flash插件，所以这里安装的flash插件主要是为了firefox。

sudo rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
sudo yum install flash-plugin
```

### rar　extract

> http://www.rarsoft.com/download.htm

```
tar -xzpvf rarlinux-3.2.0.tar.gz
cd rar
make
make install

解压方法：unrar  x  文件名.rar

```
reference
> http://blog.chinaunix.net/uid-7336769-id-2059285.html

### disable ipv6
```
# vim /etc/sysctl.conf

Put the following entry to disable IPv6 for all adapter.

  net.ipv6.conf.all.disable_ipv6 = 1

For particular adapter. (If the network card name is eno16777736).

  net.ipv6.conf.eno16777736.disable_ipv6 = 1

To reflect the changes by executing the following command.

# sysctl -p
```
reference
> http://www.itzgeek.com/how-tos/linux/centos-how-tos/how-do-i-disable-ipv6-on-centos-7-rhel-7.html


### charles 桌面快捷方式

  sudo vim /usr/share/applications/charles.desktop

```
[Desktop Entry]
Name=charles
Comment=charles
Exec=/home/user_00/Downloads/charles/bin/charles
Icon=/home/user_00/Downloads/charles/icon/charles_icon.svg
Terminal=false
Type=Application
Categories=Application;Network;
```

### wireshark

```
sudo  yum install  wireshark wireshark-gnome
```

### centos 7 显卡驱动
```
yum install nvidia-x11-drv nvidia-x11-drv-32bit kmod-nvidia xorg-x11-drv-nouveau bumblebee disper
```

> 备注：bumblebee 支持管理双显卡功能

检测显卡驱动是否安装成功
```
glxinfo | grep rendering
```
如果结果是“yes”，表示显卡驱动已经安装成功

reference
> http://seisman.info/install-nvidia-drivers-under-linux.html

### mwget 多线程下载
多线程版本的wget工具， 默认开4个线程

http://sourceforge.net/projects/kmphpfm/?source=dlp

软件包依赖 openssl-devel

```
yum install openssl-devel
cd /usr/local/src/
wget http://jaist.dl.sourceforge.net/project/kmphpfm/mwget/0.1/mwget_0.1.0.orig.tar.bz2
tar -xjvf mwget_0.1.0.orig.tar.bz2
cd mwget_0.1.0.orig
./configure
make
make install
```
