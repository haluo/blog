

##依赖
```
在安装完caffe的基础上

pip install cython  
pip install easydict  
yum install opencv-python
```
##安装
```
git clone --recursive https://github.com/rbgirshick/py-faster-rcnn.git 
cd  py-faster-rcnn/lib
make

cd py-faster-rcnn\caffe-fast-rcnn
cp Makefile.config.example Makefile.config
并跟caffe中一样做修改 

make -j8 && make pycaffe
```  

##问题

```
因为这个版本所用的cudnn为旧版本的，可能与新环境的cudnn不兼容，导致出现如下错误

In file included from ./include/caffe/util/cudnn.hpp:5:0,  
                 from ./include/caffe/util/device_alternate.hpp:40,  
                 from ./include/caffe/common.hpp:19,  
                 from ./include/caffe/util/db.hpp:6,  
                 from src/caffe/util/db.cpp:1:  
/usr/local/cuda/include/cudnn.h:803:27: note: declared here  
 cudnnStatus_t CUDNNWINAPI cudnnSetPooling2dDescriptor(  
                           ^  
make: *** [.build_release/src/caffe/util/db.o] Error 1  
make: *** Waiting for unfinished jobs....  



 解决办法：
         1).将/py-faster-rcnn/caffe-fast-rcnn/include/caffe/util/cudnn.hpp 换成最新版的caffe里的cudnn的实现，即相应的cudnn.hpp.
         2).将/py-faster-rcnn/caffe-fast-rcnn/src/caffe/layer里的，所有以cudnn开头的文件，例如cudnn_lrn_layer.cu，cudnn_pooling_layer.cpp，cudnn_sigmoid_layer.cu。
   都替换成最新版的caffe里的相应的同名文件。
```













