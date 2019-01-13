# Install Caffe

**Environments**
- Ubuntu 18.04
- Anaconda 4.3.34

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
- Open and edit 'Makefile.config' [[site](https://github.com/BVLC/caffe/pull/1667)]
