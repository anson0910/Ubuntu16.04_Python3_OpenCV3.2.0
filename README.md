# Ubuntu16.04_Python3_OpenCV3.2.0
Instructions for setting up OpenCV 3.2.0 with Python 3.5 for Ubuntu 16.04

## Script:
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake pkg-config

sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python2.7-dev python3.5-dev


cd ~
wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip
unzip opencv.zip
wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
unzip opencv_contrib.zip


cd ~/opencv-3.2.0/
mkdir build
cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.2.0/modules \
    -D PYTHON_EXECUTABLE=/usr/bin/python3.5 \
    -D PYTHON3_INCLUDE=/usr/include/python3.5 \
    -D PYTHON3_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.5m.so \
    -D PYTHON3_PACKAGES_PATH=/usr/local/lib/python3.5/site-packages \
    -D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include \
    -D BUILD_EXAMPLES=ON ..

make -j8
sudo make install
sudo ldconfig

cd /usr/local/lib/python3.5/site-packages/
sudo mv cv2.cpython-35m-x86_64-linux-gnu.so cv2.so
```

## If not done already, add **/usr/local/lib/python3.5/site-packages/** to PYTHONPATH and PyCharm Interpreter Paths:
1. Add this line to **~/.bashrc**:<br>
    `export PYTHONPATH="${PYTHONPATH}:/usr/local/lib/python3.5/site-packages"`

2. In PyCharm, go to File > Settings
3.  In the left pane, choose Project:... > Project Interpreter. In the main pane on the right, click the settings symbol (gear symbol) next to the field for "Project Interpreter". Choose More in the menu that pops up. Pick the interpreter you are using for this project and click on the tree symbol at the bottom of the window (hovering over the symbol reveals it as "Show paths for the selected interpreter"). Add your path by click in the "plus" symbol.

## References
1. [http://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/](http://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/)

2. [http://stackoverflow.com/questions/17287250/install-opencv-for-python-multiple-python-versions](http://stackoverflow.com/questions/17287250/install-opencv-for-python-multiple-python-versions)

3. [http://stackoverflow.com/questions/28326362/pycharm-and-pythonpath](http://stackoverflow.com/questions/28326362/pycharm-and-pythonpath)
