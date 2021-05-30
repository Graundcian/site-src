---
title: "Nginx反向代理"
date: 2021-05-30T11:55:00+08:00
draft: true
toc: true
authors: [graundcian]
tags: [nginx]
---

配置多域名以及多端口号，多个服务部署在同一个服务器，使用不同二级域名指向不同的端口。

<!--more-->

## 子域名指向Server端口

如果一台服务器上有许多服务，除了80端口的服务外，其它端口的服务访问是只能通过显式的写出端口号访问，

例如：abc.cn:3001   

这样操作太不友好，也不美观。

我们想要的是通过域名直接访问不同端口的服务。Nginx正好擅长干这事儿，使用子域名区分服务 的方式，然后使用 Nginx 做反向代理，分发到不同的端口。

配置如下：**/etc/nginx/conf.d/default.conf**

```nginx
server {
        listen       80;
        server_name  *.abc.cn;
 
        if ($http_host ~* "^(.*?)\.abc\.cn$") {    #正则表达式
                set $domain $1;                     #设置变量
        }
 
        location / {
            if ($domain ~* "shop") {
               proxy_pass http://abc.cn:3001;      #域名中有shop，转发到3001端口
            }
 
            if ($domain ~* "mail") {
               proxy_pass http://abc.cn:3002;      #域名中有mail，转发到3002端口
            }
 
            tcp_nodelay     on;
            proxy_set_header Host            $host;
            proxy_set_header X-Real-IP       $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            #以上三行，目的是将代理服务器收到的用户的信息传到真实服务器上
 
            root   html;
            index  index.html index.htm;            #默认情况
 
        }
 
}
```

或者(目前也不知道那个方法比较好)

```nginx
upstream sharelist {
  server 127.0.0.1:3001;
}
server {
  listen 80;
  listen [::]:80;
  server_name shop.abc.cn;
#   client_max_body_size 1024m;
  location / {
    proxy_pass http://abc.cn:3001;
    proxy_set_header HOST $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
```



