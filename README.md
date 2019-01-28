# Install Caffe

**Environments**
- Ubuntu 18.04
- Anaconda 4.3.34
- Matlab 2018b

**Matlab Installation**
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
## Check opencv installtation and remove previous opencv version
```
$ pkg-config --modversion opencv

# If there is opencv, remove it
$ sudo apt-get purge libopencv* python-opencv
$sudo apt-get autoremove
```
## Upgrade packages
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
## Install packages that need to compile OpenCV
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
## Download OpenCV-3.4.1 and OpenCV-contrib-3.4.1. [[opencv](https://opencv.org/opencv-3-4-1.html)][[opencv-contrib](https://github.com/opencv/opencv_contrib/releases?after=3.4.1)]
## Upzip those two files under the 'opencv' folder.
```
(dir.)/opencv$ ls -d */
opencv-3.4.1/ opencv_contrib-3.4.1/
```
## Move to the opencv-3.4.1 directory and make 'build' directory. We're going to compile opencv file in the build directory.
```
(dir.)/opencv$ cd opencv-3.4.1/
(dir.)/opencv/opencv-3.4.1$ mkdir build
(dir.)/opencv/opencv-3.4.1$ cd build
(dir.)/opencv/opencv-3.4.1/build$
```
## Compile OpenCV with cmake.
```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_TBB=OFF \
-D WITH_IPP=OFF \
-D WITH_1394=OFF \
-D BUILD_WITH_DEBUG_INFO=OFF \
-D BUILD_DOCS=OFF \
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
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-8.0 \
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
- Check the numbder of CPU process cores before compile.
```
$ cat /proc/cpuinfo | grep processor | wc -l
16
```
- Compile with make commands.
```
(dir.)/opencv/opencv-3.4.1/build$ make -j16
```

**Caffe installation**
- Download source file [[BVLC](https://github.com/BVLC/caffe)]
- Create a virtual enviroment and install packages.
```
conda create -n caffe_py2.7 python=2.7
source activate caffe_py2.7
conda install -c conda-forge opencv=2.4   # install opencv 2.4
```
##### package list
```
- Cython
- numpy
- scipy
- scikit-image
- matplotlib
- ipython
- h5py
- leveldb
- networkx
- nose
- pandas
- python-dateuil
- protobuf
- python-gflags
- pyyaml
- pillow
- six
```
- Move to the caffe directory and copy 'Makefile.config.example' to 'Makefile.config'
```
cd @caffe_directory
cp Makefile.config.example Makefile.config
```
- Open and edit 'Makefile.config'
```
USE_CUDNN := 1
MATLAB_DIR := /usr/local
WITH_PYTHON_LAYER := 1
USE_PKG_CONFIG := 1

# Comment the PYTHON-PATH
ANACONDA_HOME := $(HOME)/anaconda
PYTHON_INCLUDE := $(ANACONDA_HOME)/include\
                  $(ANACONDA_HOME)/include/python2.7\
                  $(ANACONDA_HOME)/lib/python2.7/site-packages/numpy/core/include\
PYTHON_LIB := $(ANACONDA_HOME)/lib
```

- Complie 
```
>> make clean
>> make all
>> make test
>> sudo gedit ~/.bashrc
# Add 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64" at the bottom
```
**Compile Error**
- 'fatal error : pyconfig.h: No such file or directory'
```
sudo apt-get install python-dev libxml2-dev libxslt-dev
```
-
