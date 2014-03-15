---
layout: post
title: "每天一个linux命令(25)之mkfs"
description: "linux命令mkfs"
category: 每天一个linux命令
tags: [linux, command]
---

`fdisk`是给磁盘分区的，分区完毕后自然就是要进行文件系统的格式化。格式化的命令就是`mkfs`，`make file system`。

`mkfs`其实十个综合命令，比如当执行`mkfs -t ext4...`时,系统会去调用`mkfs.ext4`这个命令来完成格式化操作。

##格式

```sh
mkfs [-t 文件系统格式] 设备文件名
```

##例子

