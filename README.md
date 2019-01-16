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
-- Write the following format on the text editor.
```
[Desktop]
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
-- Save it on '/home/user/desktop'
-- Check 'Allow executing file as program' on the properties.

**Installation**
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
