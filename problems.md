#1.Ubuntu Error : “The partition table format in use on your disks normally requires you to create a separate partition for boot loader code”
解决办法：添加一个分区，选择EFI，500M左右即可
Keep Boot mode in BIOS with "UEFI mode" go with the "Install Ubuntu" Option. Choose Something Else option.
1)Create a EFI Partition of around 500mb
2)Create a EXT4 Partition of your wish (100gb or 200gb) for installing Ubuntu and Mount it to / (Slash)
3)If you want to use swap partition, create a swap partition with 2 times of your RAM.
4)If you want to give additional space for home folder create a EXT4 partition of your wish and mount it to /home.
5)leave the remaining place unallocated as you can make them after installation.
6)select the device for boot loader from the drop down option at bottom of the window as /dev/sdX (X is a variable) replace X with your 7)intended drive. if you have two drives they may be named sda and sdb. this is very important. and click "Install Now"
8)Note: steps 3 & 4 are not mandatory.

#2.ubuntu时间不对
1）先查看当前系统时间和时区
date -R
2）选择时区（按提示依次选择Asia-China-Beijing
tzselect
3）复制文件到/etc目录下
sudo cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
4)再次查看时间
date -R

#3.环境配置
（参考：https://github.com/liyuxiaoboy/environment/blob/master/environment）
https://github.com/gaoxiang12/slambook/tree/master/3rdparty  下载一些库

slam14
sudo apt-get install freeglut3-dev
sudo apt install libglew-dev
sudo apt-get install libboost-dev libboost-thread-dev libboost-filesystem-dev

//install cmake：
sudo apt install cmake

//install g++：
sudo apt-get install g++

//install Eigen:
sudo apt-get install libeigen3-dev

//install git
sudo apt install git

//Sophus
cd /usr/local/include
git clone https://github.com/strasdat/Sophus.git

cd Sophus
mkdir build
cd build
cmake ..
make

//install pangolin
sudo git clone https://github.com/stevenlovegrove/Pangolin.git
 
cd Pangolin
mkdir build
cd build
cmake -DCPP11_NO_BOOST=1 ..
make -j
sudo make install

//opcv
tar -zxvf opencv-3.4.0.tar.gz 
sudo mv opencv-3.4.0 /usr/local/include

sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
sudo apt-get install libvtk5-dev libopenexr-dev
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
sudo apt-get install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip

cd opencv-3.4.0
mkdir build
cd build
cmake ..
make -j4
sudo make install

//pcl
sudo apt install libpcl-dev
sudo apt install pcl-tools
sudo apt-get install libproj-dev

//ceres
sudo apt-get install libgoogle-glog-dev
// BLAS & LAPACK
sudo apt-get install libatlas-base-dev

// SuiteSparse and CXSparse (optional)
// - If you want to build Ceres as a *static* library (the default)
//   you can use the SuiteSparse package in the main Ubuntu package
//   repository:
sudo apt-get install libsuitesparse-dev

tar -zxvf ceres-solver.tar.gz
sudo mv ceres-solver /usr/local/include
cd ceres-solver
mkdir build
cd build
cmake ..
make -j3
sudo make install

//g2o
sudo apt-get install libqt4-dev libqglviewer-dev libsuitesparse-dev  libcholmod3.0.6 libcxsparse3.1.4

tar -zxvf g2o.tar.gz
sudo mv g2o /usr/local/include
cd g2o
mkdir build
cd build
cmake ..
make -j3
sudo make install

#4.循环登录：输入密码后进入不了桌面，又重新退回输入密码界面
我是因为要用nvidia-smi查看显卡信息，但是命令不存在，所以跟着一篇博客卸载了显卡驱动导致循环登录
弄了一整个中午+下午
pre-know：
control+shift+f1 可以进入shell界面 
control+shift+f1到f6都可以进入不同的tty界面
control+shift+f7可以回到图形界面
正文：
http://www.bewindoweb.com/179.html 这篇非常有用，因为这篇才发现是显卡驱动的问题，其中内核版本先不用管，之后装不了看提示再说。
但是到安装run文件会出现问题：
1）注意使用 sudo ./NVIDIA-Linux-x86_64-384.111.run –no-x-check –no-nouveau-check –no-opengl-files 安装之前要先用 sudo chmod 755 NVIDIAxxx.run 命令修改权限，不然会出现找不到命令的情况；
1）pre-install script failed：https://blog.csdn.net/u014561933/article/details/79958130 这里面讲清楚了；
2）The target kernel has CONFIG_MODULE_SIG set：https://blog.csdn.net/ksws0292756/article/details/79160742 这篇写了安装NVIDIA驱动常见的错误，里面包含了这个error。
我出现这个的原因就是安装Ubuntu是UEFI模式启动的，但是在BIOS中却打开了Security BOOT选项，我修改为传统模式启动就能解决问题。https://blog.csdn.net/lipi37/article/details/79465685 这篇里面也有这个error相应的解释。




