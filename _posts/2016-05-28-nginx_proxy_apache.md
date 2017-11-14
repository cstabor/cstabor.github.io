---
layout: post
title:  "nginx proxy apache"
date:   2016-05-28 22:36:36 +0800
categories: php
tags: nginx, php
---

```
user  user_00;
worker_processes  4;

error_log  /data/logs/nginx/error.log warn;
pid        /tmp/nginx.pid;

events {
    worker_connections  60000;
}

http {
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
        '$status $body_bytes_sent "$http_referer" '
        '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  off;

    include conf.d/upstream.conf;

    server {
        listen 80;
        server_tokens off;

        location / {
            client_max_body_size 200m;
            client_body_buffer_size 128k;

            proxy_buffering off;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;

            proxy_pass http://192.168.1.110:80/;
        }

        location /test {
            allow all;
            include conf.d/proxy.conf;
            proxy_pass http://frontend;
        }
    }
}
```
