---
layout: post
title:  "vim clipboard"
date:   2016-05-28 14:13:36 +0800
categories: vim
---

# centos 7 default vim not support system clipboard

## resolved

### detect installed vim packages

$ rpm -qa | grep vim
```
vim-halibut-1.0-10.20120803svn9601.el7.nux.noarch
vim-filesystem-7.4.160-1.el7.x86_64
vim-X11-7.4.160-1.el7.x86_64
vim-enhanced-7.4.160-1.el7.x86_64
vim-gtk-syntax-20130716-1.el7.noarch
vim-clustershell-1.7-1.el7.noarch
vim-common-7.4.160-1.el7.x86_64
vim-minimal-7.4.160-1.el7.x86_64
vim-vimoutliner-0.3.7-5.el7.noarch

```
### method

$ sudo yum install vim-enhanced vim-X11

$ vim ~/.bashrc
```
alias vim="vimx"
alias vim="vi"
```

## reason analytics
1. 默认情况下vim 只安装了vim-minimal(减少软件依赖)。而mimimal package
不支持 `clipboard` 属性.
2. 如果需要支持`clipboard` 则需要重新从源码编译vim `--with-features=huge`

## detect whether support clipboard
1. vim 中 `:echo has('clipboard')` 
2. vim --version | grep clipboard 如果发现 `-clipboard` (表示没有支持clipboard)
