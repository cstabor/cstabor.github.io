---
layout: post
title:  "git tutorial"
date:   2016-05-28 14:13:36 +0800
categories: git
---

## git 操作

1. git init
2. git add test.txt
3. git status
4. git commit -m "test message"
5. git diff test.txt


6）版本回退。
先用git log来查看需要回退的版本，也就是之前commit的id号，亦即那条SHA1信息。

git reset --hard commit_id
1
commit_id一般写SHA1值的前几个即可，git会自动查找出来。

7）从之前回到现在。
如果在版本回退后发现也不是想要的，就要从过去回到现在。此时执行git log是没有对应的版本信息的。因此就要换一个命令了，执行git reflog便可以看到之前的commit_id了，之后再git reset即可。

8）取消修改
如果在对一份文件不小心进行了一些奇怪的操作，同时自己也忘了具体是什么，也不要慌，可以撤销相应的修改。

git checkout -- test.txt
1
git checkout有两层作用，同样这里引用廖大牛的总结原话比较清楚一点：

一种是test.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是test.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。
9）删除文件
如果你执行了rm test.txt即把test.txt给删除了，同时又不想在仓库中保留，那么执行

git rm test.txt
git commit -m "remove the test.txt"
1
2
这就从仓库中把它给删了。而另外一种情况是你不小心误删的，那么也别急，checkout一下即可恢复～

git checkout -- test.txt
1
你会发现test.txt又回来了：）

3.reference
http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
