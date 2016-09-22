1.最基本的转发
```
server {
    listen       80;
    server_name  xx.xx.com;

    location / {
        proxy_pass        http://xx.xx.xx.xx:xxxx;

        proxy_set_header   Host $http_host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

2.去掉部分路由
```
server {
    listen       80;
    server_name  xx.xx.com;

    location ^~/test/ {
        rewrite "/test/(.*)" /$1  break;
        proxy_redirect     off;

        proxy_pass        http://xx.xx.xx.xx:xxxx;
        proxy_set_header  Host            $host;
        proxy_set_header  X-Real-IP       $remote_addr;
        proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

3.添加部分路由及正则匹配
```
server {
    listen       80;
    server_name  xx.xx.com;

    location  / {
        rewrite /(.*) /1.0/$1  break;
        proxy_redirect     off;

        proxy_pass        http://xx.xx.xx.xx:xxxx;

        proxy_set_header   Host $http_host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }

    location ~* ^/[0-9]\.[0-9]/ {
        proxy_pass        http://xx.xx.xx.xx:xxxx;

        proxy_set_header   Host $http_host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```
