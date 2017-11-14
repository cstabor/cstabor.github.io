---
layout: post
title:  "thinkpad e430 centos 7 wireless driver"
date:   2016-05-28 14:13:36 +0800
categories: centos 
---
## 参考

centos wireless driver

    http://elrepo.org/tiki/wl-kmod
    http://www.broadcom.com/support/?gid=1

选择
    Linux® STA 64-bit driver

compile:

    rpmbuild --rebuild --define 'packager user_00' /home/user_00/Downloads/wl-kmod-6_30_223_271-2.el7.elrepo.nosrc.rpm

error:

    make: *** /usr/src/kernels/3.10.0-229.20.1.el7.x86_64: No such file or directory.
    是由于内核版本的源代码不一致，造成，最终通过升级内核，解决。

resolved:

    yum update
    3.10.0-327.3.1.el7.x86_64

redo：

    write /home/user_00/rpmbuild/RPMS/x86_64/kmod-wl-6_30_223_271-2.el7.local.x86_64.rpm
    .....
    exit 0

## 相关资料

    https://www.rpmfind.net/linux/rpm2html/search.php?query=kernel-devel-x86_64
    https://wiki.centos.org/HowTos/Laptops/Wireless
