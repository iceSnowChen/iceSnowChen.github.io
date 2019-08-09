---
title: nginx日志分割
date: 2019-08-07 16:04:02
tags:
---

采用系统定时任务的方式来分割日志

1. 新建shell脚本，nginx_log_split.sh

   ```sh
   #!/bin/bash
   #分割nginx的日志文件
   # 设置日志文件存放目录
   LOGS_PATH=/home/web/water/nginx_access
   #备份文件名称
   YESTERDAY=$(date -d "yesterday" +%Y%m%d%H%M)
   #重命名日志文件
   mv ${LOGS_PATH}/access.log ${LOGS_PATH}/access_${YESTERDAY}.log
   mv ${LOGS_PATH}/error.log ${LOGS_PATH}/error_${YESTERDAY}.log
   ##向nginx主进程发送USER1信号。USER1信号是重新打开日志文件，kill -USER1 信号解析归nginx所有
   kill -USR1 $(cat /var/run/nginx.pid)
   ```

2. 新建定时任务，执行crontab -e

   ```shell
   [root@dooviot nginx_access]# crontab -e
   0 0 * * * /home/web/water/nginx_access/nginx_log_split.sh
   ```

   

