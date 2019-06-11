# linux下tar压缩解压命令

### tar

* 这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个
  - -c : 建立压缩档案
  - -x : 解压
  - -t : 查看内容
  - -r : 向压缩归档文件末尾追加文件
  - -u : 更新原压缩包中的文件
  - 
* 下面的参数是根据需要在压缩或解压档案时可选的
  - -z : 有gzip属性
  - -j : 有bz2属性
  - -Z : 有compress属性
  - -v : 显示所有过程
  - -O : 将文件解开到标准输出
* 参数-f是必须的
  - -f : 必须是最后一个参数，后面接档案名字
  
* 示例

```
将文件xxx打包
tar -cvf all.tar xxx

将文件new增加到包all.tar中
tar -rvf all.tar new/

更新all.tar中的xx.xx
tar -uvf all.tar xx.xx

列出all.tar全部文件
tar -tvf all.tar

解出all.tar全部文件
tar -xvf all.tar
```

### 常用命令

* 打包&解压
```
tar -cvf all.tar *.jpg
tar -xvf all.tar
```

* 打包并压缩为gzip&解压
```
tar -czvf all.tar *.jpg
tar -xzvf all.tar
```

* 打包并压缩为bz2&解压
```
tar -cjvf all.tar *.jpg
tar -xjvf all.tar
```