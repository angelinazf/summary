# MaxConnection 修改

* 调整系统的配置(需要重启机器)
```
sudo vim /etc/security/limits.conf

增加
* hard nofile 65535
* soft nofile 65535
```

* 修改systemctl中mysql.service的配置
```
sudo vim /lib/systemd/system/mysql.service

增加
LimitNOFILE=65535
LimitNPROC=65535
```

* 修改mysql的配置文件
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf

修改
max_connections        = 10000
```