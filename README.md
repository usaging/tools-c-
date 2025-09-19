# 功能介绍

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

