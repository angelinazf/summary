# ubuntu16.04完全卸载nginx

* 卸载nginx
```
sudo apt --purge remove nginx
```

* 自动删除无用的包
```
sudo apt autoremove
```

* 查找nginx相关剩余的包
```
sudo dpkg --get-selections|grep nginx
```

* 杀死nginx进程
```
ps -ef | grep nginx
sudo kill -15 xxx
```

* 全局检索nginx相关文件并删除
```
sudo  find  /  -name  nginx*
rm -r xxx
```