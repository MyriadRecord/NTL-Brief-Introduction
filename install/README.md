### NTL 安装（Unix）
本文档适用于大部分 Unix 或者类 Unix 平台（包括 Mac OSX、使用 Cygwin tools 的Windows）。  
注：本人在 ubuntu 14.04 测试验证通过。

首先，在 [NTL 官网](http://www.shoup.net/ntl/download.html)下载一份最新的 NTL 源码。例如我把我下载的ntl-6.2.1.tar.gz压缩包放到了桌面上。ubuntu 的话直接双击解压，得到 ntl-6.2.1文件夹。执行如下命令：  

    cd Desktop/
    tar -zxvf ntl-6.2.1.tar.gz （解压，如果你已经解压了请跳过这一步）  
	cd ntl-6.2.1/src
	./configure PREFIX=$HOME/sw
	make
	make check
	make install
	
	
	
	
如果不出意外，那么你可以在 $HOME/ 下发现 sw 目录, 里面有 lib、include、share 三个子文件夹。
![sw 目录](dir-sw.png)

现在，我们成功把 NTL 编译成静态链接库，编程时就可以直接引用库文件进行编程了。