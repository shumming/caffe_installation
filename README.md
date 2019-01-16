# Install Caffe

**Environments**
- Ubuntu 18.04
- Anaconda 4.3.34
- Matlab 2017a

**Matlab Installation**
- Download the matlab vitual disk files '.iso'
- Mount 'R2017a-glnxa64-dvd1.iso'.
```
sudo su
mkdir /media/mathworks
mount R2017a-glnxa64-dvd1.iso /media/mathworks -t iso9660 -o loop
cd /media/mathworks
# check the mount
ls
./install
```

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
