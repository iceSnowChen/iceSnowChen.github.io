---
title: nginx配置HTTPS
date: 2019-08-06 18:08:27
tags:
---

```nginx
 server {
    listen 443;
    server_name water.dooviot.com;
    access_log  /home/web/water/nginx_access/access.log water;
    ssl on;
    ssl_certificate  /home/web/water/vue_web/cert/2614978_water.dooviot.com.pem;
    ssl_certificate_key /home/web/water/vue_web/cert/2614978_water.dooviot.com.key;
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
       root /home/web/water/vue_web/dist;
       index index.html;
    }
    location /admin {
       proxy_pass http://39.98.70.63:9015;
       # 以下配置是获取客户端真实的ip地址
       # X-Real-IP            客户端或上一级代理ip
       # X-Real-Port          客户端或上一级端口
       # X-Forwarded-For      包含了客户端和各级代理ip的完整ip链路
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Real-Port $remote_port;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    location /developer {
       proxy_pass http://39.98.70.63:9015;
       # 以下配置是获取客户端真实的ip地址
       # X-Real-IP            客户端或上一级代理ip
       # X-Real-Port          客户端或上一级端口
       # X-Forwarded-For      包含了客户端和各级代理ip的完整ip链路
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Real-Port $remote_port;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
 }
 server {
   listen 9016;
   server_name 39.98.70.63;
   #302是临时重定向，还是由nginx进行重定向，浏览器继续把请求发送到原地址
   #301是永久重定向,由浏览器直接把请求发送到重定向后的地址
   return 302 https://water.dooviot.com$request_uri;
 }

```

