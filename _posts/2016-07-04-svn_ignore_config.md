---
layout: post
title:  "svn ignore config"
date:   2016-07-04 16:28:00 +0800
categories: linux 
---

* TOC
{:toc}

# svn ignore 配置

两种方式

1. 修改版本库属性
2. 配置svn客户端

## 修改版本库属性 

```
svn pe svn:ignore dir
or
svn propedit svn:ignore dir
```
输入

```
runtime
*.svn
```

提交

```
svn ci -m "update message" dir
```

> dir 是要设施过滤文件列表的目录，执行命令后，输入你想过滤的文件。
> 支持通配符。 这个属性是针对版本库进行修改的，故需要提交这个修改
> svn:ignore 是svn 的一个参数。

**注意**：此设置无法递归设置，即，如果dir 目录下还有子目录，需要单独设置。

## 配置svn 客户端

```
vim ~/.subversion/config
```
> 找到 miscellany 去掉此行注释。编辑global-igonres 并去掉注释。
> 此配置是对客户端的修改，对版本库没有任何影响。同时，这个配置也是全局的，使用于本地的所有svn项目。
