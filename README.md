# CAFFe
Install caffe on Ubuntu from source.

Here are some notes when I install Caffe on Ubuntu. Might be helpful later for anyone who has the same problem as mine.


### Step 1
Download source code from official Github:
git clone https://github.com/BVLC/caffe.git

### Step 2
Install dependencies: protobuf, blas, glog, boost, gflags, hdf5, lmdb, opencv, leveldb
sudo apt-get install protobuf-compiler
sudo apt-get install libblas-dev liblapack-dev
sudo apt-get install libprotobuf-dev
sudo apt-get install libgoogle-glog-dev
sudo apt-get install libboost-all-dev
sudo apt-get install libgflags-dev
sudo apt-get install libhdf5-serial-dev
sudo apt-get install liblmdb-dev
sudo apt-get install libopencv-core-dev
sudo apt-get install libleveldb-dev
sudo apt-get install libatlas-base-dev

Install OpenCV
wget https://raw.githubusercontent.com/jayrambhia/Install-OpenCV/master/Ubuntu/2.4/opencv2_4_9.sh
chmod +x opencv2_4_9.sh 
./opencv2_4_9.sh


### Step 3
Prepare the Makefile.config file by using the template Makefile.config.example

cp Makefile.config.example Makefile.config

Modify the Makefile.config and remove the comment for Anaconda (if you are using the anaconda library)

There is a bug with the hdf5 library. The error is something similar to this:
In file included from src/caffe/solver.cpp:9:0:
./include/caffe/util/hdf5.hpp:7:10: fatal error: hdf5.h: No such file or directory
 #include "hdf5.h"

To solve this error, first add to alias to these two files: (see [link](https://github.com/NVIDIA/DIGITS/issues/156) for more detail)
cd /usr/lib/x86_64-linux-gnu
sudo ln -s libhdf5_serial.so.8.0.2 libhdf5.so
sudo ln -s libhdf5_serial_hl.so.8.0.2 libhdf5_hl.so

Then modify the Makefile.config as following:
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/

There may be another error during linking.
To solve this error, add following libraries: opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs into the end of this line (line 181)

`LIBRARIES += glog gflags protobuf boost_system boost_filesystem m`
