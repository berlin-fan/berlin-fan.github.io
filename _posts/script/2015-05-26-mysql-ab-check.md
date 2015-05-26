---
layout: post
title: mysql主从复制检查
category: script
tags: [Windows , script]
description: 检查mysql复制情况
---
#数据备份脚本

```bash
#!/bin/bash
for i in `ls -F /data/txdata/ | grep '/$' | awk -F"/" {'print $1'}`
do
   echo "+++++"$i"checkinfo+++++++++++++" >>result.log
   gets_port=`mysql --defaults-file=/data/txdata/$i/my.cnf -e 'show variables like "port"' | sed 1d | awk {'print $2'}`
   gets_ip=`ifconfig eth0 | grep "inet addr" | awk -F":" {'print $2'} | awk {'print $1'}`
   getm_ip=`mysql --defaults-file=/data/txdata/$i/my.cnf -e 'show slave status\G' | grep Master_Host| awk -F":" {'print $2'}| sed s/[[:space:]]//g`
   getm_port=`mysql --defaults-file=/data/txdata/$i/my.cnf -e 'show slave status\G' | grep Master_Port| awk -F":" {'print $2'} | sed s/[[:space:]]//g`
   get_database=`mysql --defaults-file=/data/txdata/$i/my.cnf -e 'show databases' | sed 1d | grep -v "information_schema" | grep -v "mysql" | grep -v "slowlog"`
   for j in $get_database
   do
      echo  $getm_ip $getm_port $gets_ip $gets_port $j
      echo "******"$j"******">>result.log
      mk-table-checksum h=$getm_ip,u=waptx,p='(YDtx405)',P=$getm_port h=$gets_ip,u=waptx,p='(YDtx405)',P=$gets_port  -d $j | mk-checksum-filter>>result.log
    done
done
```