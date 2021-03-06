# Install Caffe

**Overview**
- [Matlab](#matlab-installation)
- [OpenCV](#opencv-installation)
- [Segmentation-CNN](#segmentation-cnn)
- [Untrimmed-Net](#untrimmed-net)

**Environments**
- Ubuntu 18.04
- Anaconda 4.3.34
- cuda 8.0 
- cudnn 7.0

# Matlab Installation
- Download the matlab. [[link](https://kr.mathworks.com/downloads/)]
- Unzip the '.zip' file.
- Type the following commands
```
sudo su
cd /mathlab_directory
./install
```
- Install the matlab. [[refer](https://kr.mathworks.com/help/install/ug/install-mathworks-software.html)]
- Make matlab icon on the desktop [[refer](http://ngee.tistory.com/404)]
  - Write the following format on the text editor.
```
[Desktop Entry]
Name=MATLAB2018b
Type=Application
Exec=/matlab-directory/
Terminal=false
Icon=/matlab-directory/
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
Name[en]=MATLAB2018b
```
  - Save it on '/home/user/desktop'
  - Check 'Allow executing file as program' on the properties.

---

# Opencv Installation
### [[reference](https://webnautes.tistory.com/1030)]
### Check opencv installtation and remove previous opencv version
```
$ pkg-config --modversion opencv

# If there is opencv, remove it
$ sudo apt-get purge libopencv* python-opencv
$ sudo apt-get autoremove
```
### Upgrade packages
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
### Install packages that need to compile OpenCV
```
$ sudo apt-get install build-essential cmake
$ sudo apt-get install pkg-config
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev
$ sudo apt-get install libv4l-dev v4l-utils
$ sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
$ sudo apt-get install libqt4-dev
$ sudo apt-get install mesa-utils libgl1-mesa-dri libqt4-opengl-dev
$ sudo apt-get install libatlas-base-dev gfortran libeigen3-dev
$ sudo apt-get install python2.7-dev python3-dev python-numpy python3-numpy
```

  - If you have "E: Unable to locate package libjasper-dev" or "E: Package 'libpng12-dev' has no installation candidate"         errors, try following commands.
```
 sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
```
### Download OpenCV-3.4.1 and OpenCV-contrib-3.4.1. [[opencv](https://opencv.org/opencv-3-4-1.html)][[opencv-contrib](https://github.com/opencv/opencv_contrib/releases?after=3.4.1)]
### Upzip those two files under the 'opencv' folder.
```
(dir.)/opencv$ ls -d */
opencv-3.4.1/ opencv_contrib-3.4.1/
```
### Check g++ and gcc versions are under 5.0
```
# Check the version
gcc --version
g++ --version
# Install 4.8 version
sudo apt-get install gcc-4.8
sudo apt-get install g++-4.8
# Create new symbolic link
sudo rm /usr/bin/gcc
sudo rm /usr/bin/g++
sudo ln -s /usr/bin/gcc-4.8 /usr/bin/gcc
sudo ln -s /usr/bin/g++-4.8 /usr/bin/g++
```
### Move to the opencv-3.4.1 directory and make 'build' directory. We're going to compile opencv file in the build directory.
```
(dir.)/opencv$ cd opencv-3.4.1/
(dir.)/opencv/opencv-3.4.1$ mkdir build
(dir.)/opencv/opencv-3.4.1$ cd build
(dir.)/opencv/opencv-3.4.1/build$
```
### Compile OpenCV with cmake.
```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_TBB=OFF \
-D WITH_IPP=OFF \
-D WITH_1394=OFF \
-D BUILD_TIFF=ON \
-D BUILD_WITH_DEBUG_INFO=OFF \
-D BUILD_DOCS=OFF \
-D ENABLE_PRECOMPILED_HEADERS=OFF \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D BUILD_EXAMPLES=OFF \
-D BUILD_TESTS=OFF \
-D BUILD_PERF_TESTS=OFF \
-D WITH_QT=ON \
-D WITH_GTK=OFF \
-D WITH_OPENGL=ON \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.4.1/modules \
-D WITH_V4L=ON  \
-D WITH_FFMPEG=ON \
-D WITH_XINE=ON \
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.0 \
-D BUILD_NEW_PYTHON_SUPPORT=ON \
-D PYTHON2_INCLUDE_DIR=/usr/include/python2.7 \
-D PYTHON2_NUMPY_INCLUDE_DIRS=/usr/lib/python2.7/dist-packages/numpy/core/include/ \
-D PYTHON2_PACKAGES_PATH=/usr/lib/python2.7/dist-packages \
-D PYTHON2_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so \
-D PYTHON3_INCLUDE_DIR=/usr/include/python3.6m \
-D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include/  \
-D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist-packages \
-D PYTHON3_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.6m.so\
```
### Check the numbder of CPU process cores before compile.
```
$ cat /proc/cpuinfo | grep processor | wc -l
16
```
### Compile with make commands.
```
(dir.)/opencv/opencv-3.4.1/build$ make -j16
```
---

# Segmentation-CNN
### Download source file [[link](https://github.com/zhengshou/scnn)]

## Compilation of 'C3D-v1.1/C3D-overlaploss'
### Install the following packages with ```sudo apt-get install [pakage_name]```.
```
- Cython
- numpy
- scipy
- scikit-image
- matplotlib
- ipython
- h5py
- networkx
- nose
- pandas
- python-datet-util
- python-gflags
- pyyaml
- pillow
- six
```
### Install 'leveldb', 'protobuf', 'gflags', and 'glogs' from source.
- leveldb [[ref](https://gist.github.com/dustismo/6203329)]
```
$ sudo apt-get install libsnappy-dev

$ wget https://leveldb.googlecode.com/files/leveldb-1.9.0.tar.gz
$ tar -xzf leveldb-1.9.0.tar.gz
$ cd leveldb-1.9.0
$ make
$ sudo mv libleveldb.* /usr/local/lib
$ cd include
$ sudo cp -R leveldb /usr/local/include
$ sudo ldconfig
```
- protobuf-3.6.1. [[download](https://github.com/protocolbuffers/protobuf/releases/latest
)] [[ref](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md)]
  - Download the source code.
  ```
  git clone https://github.com/protocolbuffers/protobuf/releases/latest
  cd protobuf
  ```
  - Make sure you have also cloned the submodules and generated the configure script.
  ```
  $ $ git submodule update --init --recursive
  $ ./autogen.sh
  ```
  - Build and install the protocol buffer compiler
  ```
  $ ./configure
  $ make
  $ make check    #optional
  $ sudo make install
  $ sudo ldconfig
  ```
  
- gflags [[ref](https://github.com/google/glog/wiki/Installing-Glog-on-Ubuntu-14.04)]
  - Download gflags and remove the old gflags installations
  ```
  $ git clone https://github.com/gflags/gflags
  $ mkdir build
  $ cd build
  $ sudo apt-get purge libgflags-dev
  ```
  - Compile and install the protobuf-alpha
  
  ```
  $ cmake -DGFLAGS_NAMESPACE=gflags -DCMAKE_CXX_FLAGS=-fPIC ..
  $ make
  $ sudo make install
  $ sudo ldconfig
  ```
  
- glogs [[ref](https://github.com/google/glog/wiki/Installing-Glog-on-Ubuntu-14.04)]
  - Get the source code and move to the directory.
  ```
  git clone https://github.com/google/glog
  cd glog
  ```
  - Compile the glogs.
  ```
  $ ./autogen.sh
  $ ./configure
  $ make -j16
  $ sudo make install
  $ sudo ldconfig
  ```
### Update the 'caffe/include/caffe/util/cudnn.hpp' [[ref](https://github.com/BVLC/caffe/blob/master/include/caffe/util/cudnn.hpp)]
### Move to the caffe directory and copy 'Makefile.config.example' to 'Makefile.config'
```
cd @caffe_directory
cp Makefile.config.example Makefile.config
```
### Open and edit 'Makefile.config'
```
# uncomment following lines
USE_CUDNN := 1
WITH_PYTHON_LAYER := 1
```

### Complie 
```
$ cd (caffe directory)
$ mkdir build
$ cd build/
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CUDA_TOOLKIT_INCLUDE=/usr/local/cuda-8.0/include \
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-8.0 \
-D OpenCV_DIR=/media/sumin/2E06B41C06B3E34F/opencv/opencv-3.4.1/build .. \
$ make -j16
```

**Compile Error**
- 'This support is currently experimental, and must be enabled with the -std=c++11 or -std=gnu++11 compiler options.'
  -- Put the following line in CMakeLists.txt
  ```
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  ```
- 'fatal error : pyconfig.h: No such file or directory'
```
export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:/home/sumin/anaconda3/envs/caffe_py27/include/python2.7"
```
- Video error [[link](https://github.com/facebook/C3D/issues/253)]
- 'fatal error: pyconfig.h: No such file or directory' [[ref](https://github.com/okfn/piati/issues/65)]
```
export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:/home/sumin/anaconda3/envs/caffe_py27/include/python2.7/"
```
---

# Untrimmed-Net 
## Donwload the files [[link1](https://github.com/wanglimin/UntrimmedNet)] [[link2](https://github.com/yjxiong/caffe/tree/untrimmednet)]

## Need gcc-4.9 for Matlab 2017b. You can check the right version of gcc for your matlab version. [[ref](https://kr.mathworks.com/support/requirements/previous-releases.html)]
- Matlab 2017b
- gcc-4.9.3
- cuda 9.0
- cudnn 7.0

## Install gcc-4.9 [[ref](https://stackoverflow.com/questions/48398475/fail-to-install-gcc-4-9-in-ubuntu17-04)]
```
mkdir ~/Downloads/gcc-4.9-deb && cd ~/Downloads/gcc-4.9-deb

wget http://launchpadlibrarian.net/247707088/libmpfr4_3.1.4-1_amd64.deb
wget http://launchpadlibrarian.net/253728424/libasan1_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728426/libgcc-4.9-dev_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728314/gcc-4.9-base_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728399/cpp-4.9_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728404/gcc-4.9_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728432/libstdc++-4.9-dev_4.9.3-13ubuntu2_amd64.deb
wget http://launchpadlibrarian.net/253728401/g++-4.9_4.9.3-13ubuntu2_amd64.deb

sudo dpkg -i gcc-4.9-base_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i libmpfr4_3.1.4-1_amd64.deb
sudo dpkg -i libasan1_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i libgcc-4.9-dev_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i cpp-4.9_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i gcc-4.9_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i libstdc++-4.9-dev_4.9.3-13ubuntu2_amd64.deb
sudo dpkg -i g++-4.9_4.9.3-13ubuntu2_amd64.deb
```

## Check gcc-4.9 and g++-4.9 in '/usr/bin' and make symbolic link.
```
$ cd /usr/bin
$ sudo rm gcc g++
$ sudo ln -s gcc-4.9 gcc
$ sudo ln -s g++-4.9 g++
# version check
$ gcc --version
$ g++ --version
```

### Update the 'caffe/include/caffe/util/cudnn.hpp' [[ref](https://github.com/BVLC/caffe/blob/master/include/caffe/util/cudnn.hpp)]

## Make a 'build' directory.
```
$ mkdir build
$ cd build
```

## Compile files and install.
```
$ cmake .. -DUSE_MPI=ON \
-D CUDA_TOOLKIT_INCLUDE=/usr/local/cuda-9.0/include \
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.0 \
-D OpenCV_DIR=/media/sumin/2E06B41C06B3E34F/opencv/opencv-3.4.1/build ..\
-D BUILD_matlab=ON \
-D Matlab_DIR=/usr/local/MATLAB/R2017b \
$ make install
```
- If you have H5LT error, edit 'caffe/cmake/Dependencies.cmake'. [[ref](https://devtalk.nvidia.com/default/topic/1037599/jetson-tx2/installation-of-caffe-error/)]
```
---  list(APPEND Caffe_LINKER_LIBS ${HDF5_LIBRARIES})
+++  list(APPEND Caffe_LINKER_LIBS ${HDF5_LIBRARIES} ${HDF5_HL_LIBRARIES})
```
##
```
mpirun -np 1 ./install/bin/caffe test --gpu=0 \
--solver="../../UntrimmedNet-master/models/solver.prototxt" \
--model="../../UntrimmedNet-master/models/model.prototxt" \
--weights="../../UntrimmedNet-master/models/weights.caffemodel" ..\
```


