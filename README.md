# OpenCV_4.5.1-on-Ubuntu_20.10
#Installation of OpenCV on Ubuntu

#In order to compile OpenCV on Ubuntu some steps are required and outlined below.

```
apt-get install python3-venv
sudo apt-get install python3-venv
```
#To create a virtual environment use:

```
python3 -m venv --system-site-packages ./venv
```
#and to activate it use:

```
source ./venv/bin/activate
```

#Download the source:

```
mkdir ~/opencv_build && cd ~/opencv_build
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```
Change into the build directory here the build ist started:

```
cd ~/opencv_build/opencv
mkdir build && cd build
```
#Install required dependencies:
```
sudo apt-get install build-essential checkinstall yasm
sudo apt-get install cmake git gfortran libgtk2.0-dev libgtk-3-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev jasper libdc1394-22-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev libx265-dev
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install libwebp-dev
sudo apt-get install cmake-curses-gui
sudo apt install qtcreator
sudo apt install qt5-default

sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio

sudo apt -y install libtiff5-dev
sudo apt -y install libxine2-dev
sudo apt -y install libfaac-dev libmp3lame-dev libtheora-dev
sudo apt -y install libvorbis-dev
sudo apt -y install libopencore-amrnb-dev libopencore-amrwb-dev
sudo apt -y install libavresample-dev
sudo apt -y install x264 v4l-utils
sudo apt -y install libprotobuf-dev protobuf-compiler
sudo apt -y install libgoogle-glog-dev libgflags-dev
sudo apt -y install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen
sudo apt-get install libqt5x11extras5-dev qttools5-dev
sudo apt-get install openexr libopenexr-dev
sudo apt-get install libx11-dev libboost-python-dev
```

#In the build directory execute the following cmake. Directories need to be changed as neeed will be.
The Flags Enable Non Free Libraries and create the opencv.pc file which is required.
Only if all dependencies are fullfilled the libary file will be located under build/lib/python:

```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D PYTHON2_NUMPY_INCLUDE_DIRS=/home/user_name/Development/venv/lib/python3.8/site-packages/numpy/core/include/numpy/ \
-DOPENCV_PC_FILE_NAME=opencv.pc \
-D OPENCV_EXTRA_MODULES_PATH=./opencv_contrib/modules \
-D PYTHON3_LIBRARY=/home/user_name/Development/venv/lib/python3.8/site-packages \
-D PYTHON3_INCLUDE_DIR=/usr/include/python3.8    \
-D PYTHON3_EXECUTABLE=/home/user_name/Development/venv/bin/python3 \
-D BUILD_opencv_python2=OFF \
-D BUILD_opencv_python3=ON  \
-D INSTALL_PYTHON_EXAMPLES=ON  \
-D INSTALL_C_EXAMPLES=OFF \
-D OPENCV_GENERATE_PKGCONFIG=YES \
-D BUILD_EXAMPLES=ON  \
-D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib-master/modules ../opencv-master \
-D OPENCV_ENABLE_NONFREE=ON  \
-DCMAKE_CXX_COMPILER=/usr/bin/c++ \
-DCMAKE_C_COMPILER=/usr/bin/cc  \
-S ../opencv-master \
-B .
```

#You can use a graphical tool to edit the config parameters:

```
ccmake ../opencv-master
```

#Start make with number of Cores -4:

```
make -j4

```

#Start installation:

```
sudo make install
```
Go to the build/lib/pyhton directory and copy the generated .so file to cv2.so:

```
cd /lib/python
cp cv2.cpython-38-x86_64-linux-gnu.so cv2.so
```

#Change directory to your virtual environment:

```
cd /home/user_name/Development/venv/lib/python3.8/site_packages
```
#and copy the cv2.so file in there:

```
mv /home/user_name/Downloads/build/lib/python3/cv2.so .
```

#Update the config and test the installation:

```
sudo ldconfig
python3 -c "import cv2; print(cv2.__version__)"
```


#This should now have successfully created the OpenCV packages in order to use it.
