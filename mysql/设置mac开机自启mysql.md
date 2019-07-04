# mac设置mysql开机自启

* 编辑启动文件
```
sudo vim /Library/LaunchDaemons/com.mysql.mysql.plist
```
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>KeepAlive</key>
    <true/>
    <key>Label</key>
    <string>com.mysql.mysqld</string>
    <key>ProgramArguments</key>
    <array>
    <string>/usr/local/mysql/bin/mysqld_safe</string>
    <string>--user=root</string>
    </array>
  </dict>
</plist>
```
* 加载启动文件
```
sudo launchctl load -w /Library/LaunchDaemons/com.mysql.mysql.plist  
```

