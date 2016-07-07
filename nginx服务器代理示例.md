//把指定路由转发到某一服务器的某一端口
```
location ^~/statistics/ {
    proxy_pass        http://192.168.1.2:9000;
    proxy_set_header  Host            $host;
    proxy_set_header  X-Real-IP       $remote_addr;
    proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
}

location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```

//转发某一域名下的所有请求
```
listen 80;
server_name xx.xx.com;

location / {
    proxy_redirect off;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://192.168.1.2:9000;
}
access_log /var/log/nginx/a.com_access.log;
```
