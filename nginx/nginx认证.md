# nginx基础认证

* 安装apache2-utils

```
sudo apt-get install apache2-utils
```

* 增加用户

```
htpasswd -bc .passwd.db username pwd
```

* nginx配置

```
location / {
    auth_basic "wabsite-name";
    auth_basic_user_file /home/ubuntu/.passwd.db;
    ...
}
```