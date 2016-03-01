---
layout: post
title: "简单的使用 sqoop 将hive sql 查询数据数据导入到 mysql"
description: ""
category: 
theme:
  name: twitter
tagline: 让工作更简单
tags: [hive, sqoop, sql]
---

{% include JB/setup %}


# shell 脚本实现 hive sql 到 mysql

```shell
#!/bin/env bash
export HADOOP_HOME=/opt/cloudera/parcels/CDH-5.5.1-1.cdh5.5.1.p0.11
HADOOP_BIN=$HADOOP_HOME/bin
SQL_STORE=sql
cdate=`date -d "1 day ago" +"%Y-%m-%d"`

db_user=bi
db_port=3306
db=db
db_host="ip"
db_pswd="passwd"
mysqljdbc="jdbc:mysql://${db_host}:${db_port}/$db \
                --username $db_user \
                --password $db_pswd"

filename=$1
table=`basename ${filename%.*}`
echo "$table"
swap_file=${cdate}_${table}
db_table="bi_${table}"
cloumns=`mysql -u${db_user} \
               -P${db_port} \
               -h${db_host} \
               -p${db_pswd} \
               -e "SELECT substring(group_concat(COLUMN_NAME),4) \
                   FROM information_schema.COLUMNS c \
                   WHERE c.TABLE_NAME = \"${db_table}\" \
                         and table_schema = \"${db}\"" | tail -n 1`
echo "$cloumns"
$HADOOP_BIN/hdfs dfs -rm -r /data/swap/$swap_file

$HADOOP_BIN/hive  -hiveconf swap_file=$swap_file  -hiveconf cdate=$cdate -f $filename

$HADOOP_BIN/bin/hdfs dfs -cat /data/swap/$swap_file/*
$HADOOP_BIN/sqoop \
    export --connect $mysqljdbc \
           --table bi_$table \
           --m 1 \
           --export-dir /data/swap/$swap_file \
           --columns $cloumns \
           --input-fields-terminated-by '\001'
```



