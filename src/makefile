########################
# 开发框架头文件路径。
PUBINCL = -I/project/public

# 开发框架cpp文件名，直接和程序的源代码文件一起编译，没有采用链接库，是为了方便调试。
PUBCPP = /project/public/_public.cpp

##################################################
# oracle头文件路径
ORAINCL = -I$(ORACLE_HOME)/rdbms/public -I/project/public/db/oracle

# oracle库文件路径
ORALIB =  -L$(ORACLE_HOME)/lib -L.

# oracle的oci库
ORALIBS = -lclntsh

# 开发框架oracle的cpp文件名，这里直接包含进来，没有采用链接库，是为了方便调试。
ORACPP = /project/public/db/oracle/_ooci.cpp
##################################################

# 编译选项
CFLAGS = -g
#CFLAGS = -O2

# 输出目录
BINDIR = ../bin

# 确保bin目录存在
$(shell mkdir -p $(BINDIR))

all: $(BINDIR)/procctl $(BINDIR)/checkproc $(BINDIR)/deletefiles $(BINDIR)/gzipfiles \
     $(BINDIR)/ftpgetfiles $(BINDIR)/ftpputfiles $(BINDIR)/tcpputfiles $(BINDIR)/fileserver \
     $(BINDIR)/tcpgetfiles $(BINDIR)/dminingoracle $(BINDIR)/xmltodb $(BINDIR)/deletetable \
     $(BINDIR)/migratetable $(BINDIR)/syncref $(BINDIR)/syncinc $(BINDIR)/inetd \
     $(BINDIR)/rinetd $(BINDIR)/rinetdin $(BINDIR)/webserver

$(BINDIR)/procctl: procctl.cpp
	g++ $(CFLAGS) -o $@ procctl.cpp

$(BINDIR)/checkproc: checkproc.cpp
	g++ $(CFLAGS) -o $@ checkproc.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/deletefiles: deletefiles.cpp
	g++ $(CFLAGS) -o $@ deletefiles.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/gzipfiles: gzipfiles.cpp
	g++ $(CFLAGS) -o $@ gzipfiles.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/ftpgetfiles: ftpgetfiles.cpp
	g++ $(CFLAGS) -o $@ ftpgetfiles.cpp $(PUBINCL) $(PUBCPP) /project/public/libftp.a /project/public/_ftp.cpp

$(BINDIR)/ftpputfiles: ftpputfiles.cpp
	g++ $(CFLAGS) -o $@ ftpputfiles.cpp $(PUBINCL) $(PUBCPP) /project/public/libftp.a /project/public/_ftp.cpp

$(BINDIR)/tcpputfiles: tcpputfiles.cpp
	g++ $(CFLAGS) -o $@ tcpputfiles.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/fileserver: fileserver.cpp
	g++ $(CFLAGS) -o $@ fileserver.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/tcpgetfiles: tcpgetfiles.cpp
	g++ $(CFLAGS) -o $@ tcpgetfiles.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/dminingoracle: dminingoracle.cpp
	g++ $(CFLAGS) -o $@ dminingoracle.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP)

$(BINDIR)/xmltodb: xmltodb.cpp _tools.cpp
	g++ $(CFLAGS) -o $@ xmltodb.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP) _tools.cpp

$(BINDIR)/deletetable: deletetable.cpp
	g++ $(CFLAGS) -o $@ deletetable.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP)

$(BINDIR)/migratetable: migratetable.cpp _tools.cpp
	g++ $(CFLAGS) -o $@ migratetable.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP) _tools.cpp

$(BINDIR)/syncref: syncref.cpp _tools.cpp
	g++ $(CFLAGS) -o $@ syncref.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP) _tools.cpp

$(BINDIR)/syncinc: syncinc.cpp _tools.cpp
	g++ $(CFLAGS) -o $@ syncinc.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP) _tools.cpp

$(BINDIR)/inetd: inetd.cpp
	g++ $(CFLAGS) -o $@ inetd.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/webserver: webserver.cpp
	g++ $(CFLAGS) -o $@ webserver.cpp $(PUBINCL) $(PUBCPP) $(ORAINCL) $(ORALIB) $(ORALIBS) $(ORACPP) -lpthread

$(BINDIR)/rinetd: rinetd.cpp
	g++ $(CFLAGS) -o $@ rinetd.cpp $(PUBINCL) $(PUBCPP)

$(BINDIR)/rinetdin: rinetdin.cpp
	g++ $(CFLAGS) -o $@ rinetdin.cpp $(PUBINCL) $(PUBCPP)

clean:
	rm -rf $(BINDIR)/procctl $(BINDIR)/checkproc $(BINDIR)/deletefiles $(BINDIR)/gzipfiles
	rm -rf $(BINDIR)/ftpgetfiles $(BINDIR)/ftpputfiles $(BINDIR)/tcpputfiles $(BINDIR)/fileserver
	rm -rf $(BINDIR)/tcpgetfiles $(BINDIR)/dminingoracle $(BINDIR)/xmltodb $(BINDIR)/deletetable
	rm -rf $(BINDIR)/migratetable $(BINDIR)/syncref $(BINDIR)/syncinc $(BINDIR)/inetd
	rm -rf $(BINDIR)/rinetd $(BINDIR)/rinetdin $(BINDIR)/webserver

.PHONY: all clean