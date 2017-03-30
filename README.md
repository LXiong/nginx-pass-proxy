# Why we use nginx reverse proxy

Currentry, many application choice architecure "Microservices Architecture"(MSA).

In MSA, each applications deploy as independent web applicaitons. But almost users don't know application architecture. Users want to use each web application as an integrated application.

We need to integrate each applicaions as an application by URL.

# What is path proxy

The path proxy integrate each applications URL by "path".

e.g. 

|Applciation|Application Address|Proxy Address|
|-----------|-------------------|-------------|
|Catalog    |10.0.0.1           |https://www.eshop.com/catalog|
|Basket     |10.0.0.2           |https://www.eshop.com/basket|
|Order      |10.0.0.3           |https://www.eshop.com/order|


# How to configure nginx.

The nginx Reverse Proxy configured by nginx.conf.
e.g. Path proxy from www.eshop.com to 10.0.0.1

```
http {
    include /etc/nginx/mime.types;
    default_type    application/octet-stream;

    sendfile    on;
    keepalive_timeout   65;
    server{
        server_name    www.eshop.com;
        proxy_set_header    Host    $http_host;

        location /catalog/ {
            proxy_pass    http://10.0.0.1/;
        }
    }
}

```

Reverse Proxy configuration in "http" sections.
In the "location" section define proxy pass and server location.

# How to run nginx path proxy

Run docker container with conf file.

```
 docker run --name nginx-path-proxy -v ./nginx.conf:/etc/nginx/nginx.conf:ro -d nginx
```