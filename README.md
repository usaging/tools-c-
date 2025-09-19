# 介绍

# procctl

服务程序的调度程序，周期性启动服务程序或shell脚本。

Using:./procctl timetvl program argv ...

fork子进程执行任务，父进程等待子进程退出，然后sleep一段时间，再次fork。

# checkproc

检查后台服务程序是否超时，如果已超时，就终止它。

Using:./checkproc logfilename

遍历共享内存中全部的进程记录，如果进程已超时，终止它。

# gzipfiles

这是一个工具程序，用于压缩历史的数据文件或日志文件。

Using:./gzipfiles pathname matchstr timeout

本程序把pathname目录及子目录中timeout天之前的匹配matchstr文件全部压缩，timeout可以是小数。

# deletefiles

这是一个工具程序，用于删除历史的数据文件或日志文件。

Using:./deletefiles pathname matchstr timeout

本程序把pathname目录及子目录中timeout天之前的匹配matchstr文件全部删除，timeout可以是小数。

# ftpputfiles

用于将本地文件上传到FTP服务器。

## 关键组件

1. 参数结构体 (st_arg)

- 远程服务端的IP和端口
- 传输模式，1-被动模式，2-主动模式
- 远程服务端ftp的用户名
- 远程服务端ftp的密码
- 远程服务端存放文件的目录
- 本地文件存放的目录
- 待上传文件匹配的规则
- 上传后客户端文件的处理方式
- 上传后客户端文件的备份目录
- 已上传成功文件名清单
- 进程心跳的超时时间
- 进程名

2. 核心容器
map<string, string> mfromok: 存放已上传成功文件的信息

list<struct st_fileinfo> vfromdir: 本地目录中的文件列表

list<struct st_fileinfo> vtook: 本次不需要上传的文件

list<struct st_fileinfo> vupload: 本次需要上传的文件

3. 核心函数

loadlocalfile(): 加载本地文件列表

loadokfile(): 加载已上传成功文件信息

compmap(): 比较文件列表，确定需要上传的文件

writetookfile(): 写入已上传文件信息

appendtookfile(): 追加上传成功的文件记录

## 核心工作流程

1. FTP连接和认证
   
2. 获取本地文件列表

3. 增量上传处理（ptype=1）

加载已上传文件信息到容器mfromok。

比较文件列表，确定需要上传的文件。

更新已上传文件信息。

4. 文件上传

遍历需要上传的文件列表。

拼接本地和远程文件路径。

使用ftp.put()方法上传文件。

处理上传后的本地文件（根据ptype参数）。

5. 文件处理

ptype=1: 记录已上传文件信息。

ptype=2: 删除本地文件。

ptype=3: 将本地文件移动到备份目录。

# ftpgetfiles.cpp

用于从FTP服务器下载文件到本地目录。

## 关键组件

1. 参数结构体 (st_arg)

- 远程服务端的IP和端口
- 传输模式，1-被动模式，2-主动模式
- 远程服务端ftp的用户名
- 远程服务端ftp的密码
- 远程服务端存放文件的目录
- 本地文件存放的目录
- 待下载文件匹配的规则
- 下载后服务端文件的处理方式
- 下载后服务端文件的备份目录
- 已下载成功文件信息存放的文件
- 是否需要检查服务端文件的时间
- 进程心跳超时的时间
- 进程名

这个结构体定义了FTP文件下载的所有配置参数。

2. 核心容器

map<string, string> mfromok: 存放已下载成功文件的信息。

list<struct st_fileinfo> vfromnlist: 下载前列出服务端文件名的容器。

list<struct st_fileinfo> vtook: 本次不需要下载的文件的容器。

list<struct st_fileinfo> vdownload: 本次需要下载的文件的容器。

3. 核心函数
   
loadokfile(): 加载已下载成功文件信息。

loadlistfile(): 加载FTP服务器文件列表。

compmap(): 比较文件列表，确定需要下载的文件。

writetookfile(): 写入已下载文件信息。

appendtookfile(): 追加下载成功的文件记录。

## 核心工作流程

1. 初始化阶段

2. FTP连接和认证

登录FTP服务器

切换到远程目录

3. 获取文件列表

使用ftp.nlist()方法获取服务器文件列表

将文件列表保存到本地临时文件

加载文件列表到容器vfromnlist

4. 增量下载处理（ptype=1）

加载已下载文件信息到容器mfromok

比较文件列表，确定需要下载的文件

更新已下载文件信息

5. 文件下载

遍历需要下载的文件列表

拼接远程和本地文件路径

使用ftp.get()方法下载文件

处理下载后的文件（根据ptype参数）

6. 文件处理

ptype=1: 记录已下载文件信息

ptype=2: 删除服务器上的文件

ptype=3: 将服务器文件移动到备份目录


