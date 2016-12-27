**一、实验任务**

在Ubuntu 14.04中安装ROS

**二、实验步骤**

**1、安装依赖项**

执行以下指令:

	sudo apt-get install -y google-mock 
	libboost-all-dev  
	libeigen3-dev 
	libgflags-dev 
	libgoogle-glog-dev 
	liblua5.2-dev 
	libprotobuf-dev  
	libsuitesparse-dev 
	libwebp-dev 
	ninja-build 
	protobuf-compiler 
	python-sphinx  
	ros-indigo-tf2-eigen 
	libatlas-base-dev 
	libsuitesparse-dev 
	liblapack-dev

**2、安装ceres solver**

在home目录下新建文件夹catkin_ws，在该目录下，执行以下代码：
	
	git clone https://github.com/hitcm/ceres-solver-1.11.0.git  

打开文件夹catkin_ws/ceres-solver-1.11.0，新建文件夹build并进入，在该目录下执行以下指令：

	cmake ..
	make
	sudo make install

**3、安装cartographer**

在catkin_ws下新建文件夹cat，在该目录下，执行以下指令：

	git clone https://github.com/hitcm/cartographer.git

打开文件夹catkin_ws/cat/cartographer，新建文件夹build并进入，在该目录下执行以下指令：

	cmake ..
	make 
	sudo make install

**4、安装cartographer_ros**

进入catkin_ws的src目录下，执行以下指令:

	git clone https://github.com/hitcm/cartographer_ros.git

在catkin_ws下执行指令：

	catkin_make

**5、数据测试**

从下面链接下载文件后复制到Ubuntu:

	https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag

在终端执行指令：

	roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag

效果图:
![](https://raw.githubusercontent.com/zhanggx9/ES2016_14353387/master/lab5/ros.png)

三、实验总结

本次实验在安装依赖项ros-indigo-tf2-eigen 时出现报错无法下载，通过网上查找资料后，在安装之前执行以下指令解决了这个问题：

	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'

	wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -

	sudo apt-get update
