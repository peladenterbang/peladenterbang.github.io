# NGINX

Nginx is one of most popular web server in the world, other web server is apache, tomcat, etc., but the advantages of nginx compared from other web server is enterprise version. So that nginx often to used by large companies. Support by expert engineer is one of important to handle services with  zero down time.&#x20;

### 1. Installation

first. lets do to install nginx with simple http server.

1. install nginx&#x20;

```
## for ubuntu
apt install nginx

## for RHEL/centos 
yum install epel-releas
yum install nginx

## for fedora 
dnf install nginx
```

{% hint style="info" %}
nginx service configure location : /etc/nginx/nginc.conf

index file location : /usr/share/nginx/html/index.html or /var/www/html/

default site-available configuration : /etc/nginx/sites-available/default
{% endhint %}

2. After installing nginx check status service, makesure not any error on there

```
systemctl status nginx
```

3. simple, after service nginx running you can check with curl or access your ip address on web browser.

```
curl localhost
## or
curl <ip address>
```

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>



### 2. Nginx for Loadbalancer

to implement high availability web server we can used nginx for loadbalancer, for example :



<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

you need have 4 vm or instance to implement web server loadbalancing, 1 for proxy and 3 for upstream.

selected algorithm :&#x20;

* round-robin (default)
* ip\_hash or hash
* least\_conn
* least\_time

loadbalancing component :&#x20;

* choose algirithm&#x20;
* upstream (web server -> nginx, apache, ot tomcat)
* proxy\_pass
* health check&#x20;

**configuration :**&#x20;

1. install nginx to all node ,and after that initialization ip address to hosts file&#x20;

```
## execute on all node
apt install nginx -y

nano /etc/hosts
10.0.0.22 ca-server01
10.0.0.47 ca-server02
10.0.0.48 ca-server03
10.0.0.50 ca-server04
```

2. access to vm 02, vm 03, vm 04, edit default `index.html` .

```
## exec on vm02,wm03,vm04
nano /var/www/html/index.html
---
    <head>
    <h1> Welcome to nginx! SERVER "server number" <h1>
---

save and exit
```

3. access to vm01 to nginx proxy configuration.

```
# exec on vm01

rm /etc/nginx/conf.d/*
nano /etc/nginx/conf.d/main.conf

## copy and adjust 

upstream myServers {
    server ca-server02:80;
    server ca-server03:80;
    server ca-server04:80;
}

server {
    listen 8080;
    root /usr/share/nginx/html;

    access_log /var/log/nginx/main.access.log combined;
    error_log /var/log/nginx/main.error.log info;

    location / {
        proxy_pass http://myServers;
    }

}
```

4. then check file configuration and restart nginx service&#x20;

```
# exec on vm01
# check file configuration
root@ca-server01:~# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

# then restart service 
root@ca-server01:/etc/nginx/conf.d# nginx -s reload
root@ca-server01:/etc/nginx/conf.d#
```

5. test loadbalancer, access to your \<ip vm01>:8080 and reload several times. You can see, the page `welcome nginx` will be change to other server.

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### 3. Caching Web Server

we can configure nginx for cache request to optimizing performance.

```
## edit on your configuration domain 
nano /etc/nginx/sites-available/yourdomain.com
## add this before closing curly brace  "}" , inside server configuration {}

---
        #location ~ /\.ht {
        #       deny all;
        #}
        # Feed
        location ~* \.(?:rss|atom)$ {
          expires 1h;
          add_header Cache-Control "public";
        }
        # media
        location ~* \.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc)$ {
          expires 30d;
          access_log off;
          add_header Cache-Control "public";
        }
        # css
        location ~* \.(?:css|js)$ {
          expires 1y;
          access_log off;
          add_header Cache-Control "public";
        }


}
---

## then restart nginx services
systemctl restart nginx
```

you can adjust **expires time** according to "what you need".

### 4. NGINX SSL
