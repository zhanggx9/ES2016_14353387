一、DOL框架描述

Distributed Operation Layer : 

The distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

二、DOL安装笔记

1、安装一些必要的环境

	$	sudo apt-get update
	$	sudo apt-get install ant
	$ 	sudo apt-get install openjdk-7-jdk
	$	sudo apt-get install unzip
2、在Vmware虚拟机中下载文件systemc-2.3.1.tgz和dol_ethz.zip

	sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

	sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
3、解压文件
新建dol的文件夹 

	$	mkdir dol
将dolethz.zip解压到 dol文件夹中

	$	unzip dol_ethz.zip -d dol
解压systemc

	$	tar -zxvf systemc-2.3.1.tgz
4、编译systemc
解压后进入systemc-2.3.1的目录下

	$	cd systemc-2.3.1
新建一个临时文件夹objdir

	$	mkdir objdir
进入该文件夹objdir

	$	cd objdir
运行configure(能根据系统的环境设置一下参数，用于编译)

	$	../configure CXX=g++ --disable-async-updates
编译

	$	sudo make install
编译完后在如下文件目录

	$ cd ..  
	$ ls
中的结果为：
![](http://p1.bpimg.com/4851/c6bc565690b7d361.jpg)

记录当前的工作路径(会输出当前所在路径，记下来，待会有用)

	$	pwd
![](http://p1.bqimg.com/567571/d2ed129602c1f4b7.jpg)

5、编译dol
进入刚刚dol的文件夹

	$	cd ../dol
修改build_zip.xml文件
找到下面这段话，就是说上面编译的systemc位置在哪里，

	<property name="systemc.inc" value="YYY/include"/>
	<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
把YYY改成上页pwd的结果
然后是编译

	$	ant -f build_zip.xml all
若成功会显示build successful

6、运行第一个例子
进入build/bin/mian路径下

	$	cd build/bin/main
然后运行第一个例子

	$	ant -f runexample.xml -Dnumber=1
结果如下图所示：
![](http://p1.bqimg.com/567571/eda68a66b76d2ec2.jpg)

三、实验总结

本次实验主要使用了ubuntu，由于之前有使用过这个软件的经历，所以这次的安装配置没有遇到太大的问题，不过接触到了挺多新东西，去了解DOL框架还是花了比较多的时间。
