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
	
	
	
执行上述命令使得 NTl 被安装在了 $HOME/sw 下。你可以修改 $HOME/sw 使得 NTL 安装在其他地方（默认会安装在 /usr/local）	。
如果不出意外，那么你可以在 $HOME/ 下发现 sw 目录, 里面有 lib、include、share 三个子文件夹。其中 /include/NTL 放着 NTL 的头文件，/lib 则存放着 NTl 的静态库文件 libntl.a。
![sw 目录](dir-sw.png)

你还可以通过 GMP (the GNU Multi-Precision package) 编译 NTL 以获得更好的表现。假设在你的机器上已经安装了 GMP，而且安装路径为 /usr/local，那么你可以执行如下设置：

	./configure PREFIX=$HOME/sw NTL_GMP_LIP=on
	
如果 GMP 安装在了其他路径上，如$HOME/sw,那么：

	./configure PREFIX=$HOME/sw NTL_GMP_LIP=on GMP_PREFIX=$HOME/sw
	
或者，还可以这样：
	
	./configure DEF_PREFIX=$HOME/sw NTL_GMP_LIP=on
	
上方命令中，DEF_PREFIX 指定了所有软件的路径，默认情况下，DEF_PREFIX=/usr/local。
  
  
如果你想更更高校地完成如 GF(2)之类的多项式运算，你可能会考虑使用 gf2x 库。要使用 gf2x 库，首先你需要安装好 gf2x。同上述 GMP 一样，你需要设置 configure 的 NTL_GF2X_LIB=on。如果你把 gf2x 安装在了其他路径上，还要设置 GF2X_PREFIX=$HOME/sw（如果你的安装路径是$HOME/sw）。  
  
现在，我们成功把 NTL 编译成静态链接库，编程时就可以直接引用库文件进行编程了。
假设 `/Desktop/HelloNTL/`是你的工作目录。`HelloNTL.c`是你的源代码文件。而你按照上述说明把 NTL 安装在了 $HOME/sw 下。那么可以执行如下命令开始编译：

1. 进入工作目录。命令行输入
	
		cd /Desktop/HelloNTL
	
2. 编译源文件。
	
		g++  -I$HOME/sw/include HelloNTL.c -o HelloNTL  -L$HOME/sw/lib -lntl  -lm
	如果你想使用 GMP，请输入：
	
		g++ -I$HOME/sw/include HelloNTL.c -o HelloNTL  -L$HOME/sw/lib -lntl -lgmp  -lm
	
	如果你想使用 GMP 和 gf2x,那么：
		
		g++  -I$HOME/sw/include HelloNTL.c -o HelloNTL  -L$HOME/sw/lib -lntl -lgmp -lgf2x  -lm	