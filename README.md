# How to run nginx path proxy

Run docker container with conf file.

```
 docker run --name nginx-path-proxy -v ./nginx.conf:/etc/nginx/nginx.conf:ro -d nginx
```