---
layout: post
title: mysql主从复制检查
category: script
tags: [linux, script]
description: 检查mysql复制情况
---

只列目录
```
ls -F | grep '/$'
ls -l | grep '^d'
ls -ld */
ls -ap | grep '/'
tree -d -L 1
```

去除行首行尾空格
```
sed s/[[:space:]]//g
```

linux 设置字符集（utf-8）
```
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN"
SUPPORTED="zh_CN.UTF-8:zh_CN:zh:en_US.UTF-8:en_US:en"
SYSFONT="lat0-sun16"
```
