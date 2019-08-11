---
title: nginx执行的11个阶段
date: 2019-08-09 14:02:09
tags:
---

![1565331118625](../img/1565331118625.png)

```nginx
    location /test {
       #set属于rewrite阶段的命令
       set $a 100
       #echo属于content阶段的命令
       echo '$a'
       set $a 200
       echo '$a'
    }
```

上述输出结果：200, 200