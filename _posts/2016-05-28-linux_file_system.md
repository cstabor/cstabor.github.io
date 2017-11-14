---
layout: post
title:  "linux file system"
date:   2016-05-28 14:13:36 +0800
categories: linux 
---

### mount 查看文件系统及挂载点

> mount

```bash
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=2736700k,nr_inodes=684175,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/centos-root on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=34,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw,relatime)
nfsd on /proc/fs/nfsd type nfsd (rw,relatime)
/dev/sdb1 on /boot type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
/dev/sda1 on /data1 type ext3 (rw,relatime,seclabel,data=ordered)
/dev/mapper/centos-home on /home type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=551812k,mode=700,uid=1000,gid=1000)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)
fusectl on /sys/fs/fuse/connections type fusectl (rw,relatime)

```

### 查看inode 数

ext4 文件系统中，单个文件夹下能存储的文件数限制，取决于 inode　数

> df -i

```
Filesystem                Inodes  IUsed    IFree IUse% Mounted on
/dev/mapper/centos-root 52428800 281062 52147738    1% /
devtmpfs                  684175    516   683659    1% /dev
tmpfs                     689765    487   689278    1% /dev/shm
tmpfs                     689765    700   689065    1% /run
tmpfs                     689765     13   689752    1% /sys/fs/cgroup
/dev/sdb1                 512000    344   511656    1% /boot
/dev/sda1               30531584  99155 30432429    1% /data1
/dev/mapper/centos-home 66256896  76316 66180580    1% /home
tmpfs                     689765     31   689734    1% /run/user/1000

```

> df -Thi

```
Filesystem              Type     Inodes IUsed IFree IUse% Mounted on
/dev/mapper/centos-root xfs         50M  275K   50M    1% /
devtmpfs                devtmpfs   669K   516  668K    1% /dev
tmpfs                   tmpfs      674K   488  674K    1% /dev/shm
tmpfs                   tmpfs      674K   700  673K    1% /run
tmpfs                   tmpfs      674K    13  674K    1% /sys/fs/cgroup
/dev/sdb1               xfs        500K   344  500K    1% /boot
/dev/sda1               ext3        30M   97K   30M    1% /data1
/dev/mapper/centos-home xfs         64M   75K   64M    1% /home
tmpfs                   tmpfs      674K    31  674K    1% /run/user/1000
```

### 查看分区

> parted

```
[user@thinkpad /]$ sudo parted
GNU Parted 3.1
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) p                                                                
Model: ATA WDC WD5000LPVT-0 (scsi)
Disk /dev/sda: 500GB
Sector size (logical/physical): 512B/4096B
Partition Table: msdos
Disk Flags:

Number  Start   End    Size   Type     File system  Flags
 1      1049kB  500GB  500GB  primary  ext3

(parted)
```
