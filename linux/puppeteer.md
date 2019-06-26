# puppeteer在Ubuntu16.04的相关服务部署

* 安装node
* 安装puppeteer(同时会安装Chrome)
```
npm i puppeteer
```
* js中启动时候需要指定Chrome的执行路径
```
const browser = await puppeteer.launch({executablePath: '/home/ubuntu/bitzoom-monitor/node_modules/puppeteer/.local-chromium/linux-669486/chrome-linux/chrome'});
```
* 正常启动会报错，是因为缺失一些Chrome需要的库
```
home/ubuntu/bitzoom-monitor/node_modules/puppeteer/.local-chromium/linux-669486/chrome-linux/chrome: error while loading shared libraries: libX11-xcb.so.1: cannot open shared object file: No such file or directory
```
* 解决办法
```
查看缺失的包
ldd chrome | grep not
安装
sudo apt install -y gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget
中途可能需要
sudo apt -f install
```

##### 参考文档
* https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md
* https://techoverflow.net/2018/06/05/how-to-fix-puppetteer-error-while-loading-shared-libraries-libx11-xcb-so-1-cannot-open-shared-object-file-no-such-file-or-directory/