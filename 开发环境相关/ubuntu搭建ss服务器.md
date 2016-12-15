apt-get update
---
apt-get install python-pip
---
pip install shadowsocks
---
etc/shadowsocks.json
{
    "server":"my_server_ip",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"mypassword",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
---


/etc/rc.d/rc.local
ssserver -c /etc/shadowsocks.json -d start
