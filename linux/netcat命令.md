# netcat

* https://www.oschina.net/translate/linux-netcat-command

### 端口扫描
* 查看某IP端口开放情况
```
netcat -v ip/host port
```
* 端口扫描
```
netcat -v ip/host port1-port2
```

### 即时通信
* 假设现在有两台主机A和B，A想要和B进行简单的信息通信，那么可以指定其中一台主机作为server，绑定自己的一个端口作为通信端口
```
netcat -l port
```
* 然后将主机B作为客户端去连接主机A的1000端口（前提是要知道主机A的IP地址）
```
netcat ip port
```
* 在server端和client端都搭建好了以后，就可以互相进行即时通信 

### 文件传输
* 假设从A服务器想要传输一个文件去B服务器，可以将A作为服务端，B做为客户端
* Server A
```
netcat -l port < file.txt
```
* Client B
```
netcat -n ip port > file.txt
```
* 这里我们创建了一个服务器在A上并且重定向netcat的输入为文件file.txt，那么当任何成功连接到该端口，netcat会发送file的文件内容。
* 在客户端我们重定向输出到file.txt，当B连接到A，A发送文件内容，B保存文件内容到file.txt.
* 也可以反向操作,是一样的效果
```
netcat -l port > file.txt
netcat -n ip port < file.txt
```

### 目录传输
* 如果想要传输一个目录，那么可以归档压缩后传输
* 假设传输一个目录从A到B
* Server A
```
tar -cvf - dir | netcat -l port
```
* Client B
```
netcat -n ip port | tar -xvf -
```
* 这里在A服务器上，我们创建一个tar归档包并且通过-在控制台重定向它，然后使用管道，重定向给netcat，netcat可以通过网络发送它。
* 在客户端我们下载该归档包通过netcat管道然后打开文件。
* 还可以通过bzip2或者其他工具进行压缩
```
tar -cvf - dir | bzip2 -z | netcat -l port
netcat -n ip port | bzip2 -d | tar -xvf - 
```

### 加密发送数据
* 服务端加密数据传输(示例使用mcrypt)
* Server
```
netcat ip port | mcrypt -flush -bare -F -q -d -m ecb > file.txt
```
* Client
```
mcrypt -flush -bare -F -q -m ecb < file.txt | netcat -l port
```

### 流视频
* 虽然不是生成流视频的最好方法，但如果服务器上没有特定的工具，使用netcat，我们仍然有希望做成这件事。
* Server
```
cat video.avi | netcat -l port
* 这里我们只是从一个视频文件中读入并重定向输出到netcat客户端
```
* Client
```
netcat ip port | mplayer -vo x11 -cache 3000 -
```
* 这里我们从socket中读入数据并重定向到mplayer