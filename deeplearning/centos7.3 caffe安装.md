#centos7.3 caffe安装

##1.硬件

```
gtx1080*2  无集显

```

##2.系统
```
  centos 7.3 minimal 版本
  采用linux text  文本模式安装
  首先安装epel扩展源：
  sudo yum -y install epel-release
  然后安装python-pip
  sudo yum -y install python-pip
 
sudo yum -y install python-pip
```

##3.nvidia驱动

```
依赖包安装：
yum -y install gcc kernel-devel kernel-headers
查看依赖包版本和本机kernel版本是否一致 否则可能导致安装失败
yum -y install kernel-devel "kernel-devel-uname-r == $(uname -r)"
yum -y install kernel-headers "kernel-headers-uname-r == $(uname -r)"
 

修改 /etc/modprobe.d/blacklist.conf 
以阻止 nouveau 模块的加载
方法： 添加blacklist nouveau，注释掉blacklist nvidiafb

重新建立initramfs image文件
mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
dracut /boot/initramfs-$(uname -r).img $(uname -r)

修改/etc/inittab，使系统开机进入init 3文本模式:
将最后一行“id:5:initdefault:”修改成“id:3:initdefault:”（不包含引号）
注释：5代表系统启动时默认进入x-window图形界面，3代表默认进入终端模式。 

官网下载NVIDIA-Linux-x86_64-375.26.run
执行安装即可
```

## cuda安装

```
官方下载

cuda_8.0.61_375.26_linux-2.run centos版本

cuda_8.0.61_375.26_linux-2.run

修改环境变量

sudo vim ~/.bashrc
添加

export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

测试CUDA的sammples：

cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery 

make

sudo ./deviceQuery
```

##cudnn安装

```
下载 cudnn-8.0-linux-x64-v5.1.tgz

sudo cp cudnn.h /usr/local/cuda/include/

sudo cp lib* /usr/local/cuda/lib64/    #复制动态链接库
cd /usr/local/cuda/lib64/sudo rm -rf libcudnn.so libcudnn.so.5    #删除原有动态文件
sudo ln -s libcudnn.so.5.1.5 libcudnn.so.5  #生成软衔接
sudo ln -s libcudnn.so.5 libcudnn.so      #生成软链接
```

##安装依赖

```
通用依赖
sudo yum install protobuf-devel leveldb-devel snappy-devel opencv-devel boost-devel hdf5-devel

如果使用blas
sudo yum install atlas-devel
使用python
yum install the python-devel

剩余依赖
sudo yum install gflags-devel glog-devel lmdb-devel

如果剩余依赖无法安装 则手动安装：
# glog
wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/google-glog/glog-0.3.3.tar.gz
tar zxvf glog-0.3.3.tar.gz
cd glog-0.3.3
./configure
make && make install
# gflags
wget https://github.com/schuhschuh/gflags/archive/master.zip
unzip master.zip
cd gflags-master
mkdir build && cd build
export CXXFLAGS="-fPIC" && cmake .. && make VERBOSE=1
make && make install
# lmdb
git clone https://github.com/LMDB/lmdb
cd lmdb/libraries/liblmdb
make && make install

如果hdf5和leveldb也需要手动安装：
cd leveldb-1.7.0 
make
cp libleveldb* /usr/lib/
cp –r include/leveldb /usr/local/include


$ cd hdf5-X.Y.Z
$ ./configure --prefix=/usr/local/hdf5 <more configure_flags>
$ make
$ make check                # run test suite.
$ make install
$ make check-install
vim ~/.bashrc
export LD_LIBRARY_PATH=/usr/local/hdf5/lib:$LD_LIBRARY_PATH

```

##配置caffe

```
git clone https://github.com/BVLC/caffe.git



cp Makefile.config.example Makefile.config


`#USE_CUDNN := 1 修改成： USE_CUDNN := 1


若使用的opencv版本是3的，则
将#OPENCV_VERSION := 3 
修改为： 
OPENCV_VERSION := 3

将#WITH_PYTHON_LAYER := 1 
修改为 
WITH_PYTHON_LAYER := 1

BLAS_INCLUDE := /usr/include
BLAS_LIB := /usr/lib64/atlas


如果hdf5手动安装且找不到需要配置
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include  /usr/local/hdf5/include
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/local/hdf5/lib


 vim Makefile
 将 LIBRARIES += cblas atlas 改为 LIBRARIES += satlas tatlas



make all -j8
make runtest

```








