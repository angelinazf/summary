# mysql5.7安装

* https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/

### Ubuntu 16.04, 18.04, and 18.10
* 安装
```
sudo apt-get update
sudo apt-get install mysql-server
```
* 卸载
```
sudo apt-get remove mysql-server
sudo apt-get autoremove
// To see a list of packages you have installed from the MySQL APT repository, use the following command:
dpkg -l | grep mysql | grep ii
```