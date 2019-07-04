NCS2-and-Coral-TPU-on-aarch64
How to install NCS2 Movidius XX and Google Coral TPU on aarch64
 **1. apt-get**<br/>
sudo apt-get update && sudo apt-get upgrade<br />
sudo apt-get install build-essential cmake unzip pkg-config<br/>
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev<br/>
sudo apt-get install libxvidcore-dev libx264-dev  <br/>
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev<br/>
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev<br/>
sudo apt-get install python3-dev python3-numpy python3-pip<br/>
sudo apt-get install curl wget libssl-dev ca-certificates git libboost-regex-dev<br/>
sudo apt-get install libgtk2.0-dev pkg-config unzip automake libtool autoconf<br/>
sudo apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libgtk2.0-dev<br/>
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base libusb-1.0-0-dev<br/>
sudo apt-get install ffmpeg libjpeg-dev libtiff-dev  git  libtbb2 libtbb-dev<br/>
sudo apt-get install cython cython3 libv4l-dev<br/>
<br/>
**2. pip/python**<br/>
wget https://bootstrap.pypa.io/get-pip.py<br/>
sudo python3 get-pip.py<br/>
sudo -H  pip  install numpy<br/>
sudo -H  pip3 install Cython<br/>
<br/>
**3. Extra nice to have**
sudo apt-get install codeblocks codeblocks-contrib<br/>
sudo apt-get install spyder3<br/>
<br/>
**4. Swapfile Armbian** ( if you want to compile faster, with make -j4)<br/>
 https://linuxize.com/post/how-to-add-swap-space-on-debian-9/<br/>
 <br/>
sudo swapon --show<br/>
sudo fallocate -l 2G /swapfile<br/>
sudo dd if=/dev/zero of=/swapfile bs=1024 count=2048576<br/>
sudo chmod 600 /swapfile<br/>
sudo mkswap /swapfile<br/>
sudo swapon /swapfile<br/>

 *If you whant to make it permanent ..*<br/>
sudo nano /etc/fstab<br/>

 add<br/>
/swapfile swap swap defaults 0 0<br/>
<br/>
 **1. apt-get**
sudo apt-get update && sudo apt-get upgrade<br />
sudo apt-get install build-essential cmake unzip pkg-config<br/>
 **1. apt-get**<br/>
sudo apt-get update && sudo apt-get upgrade<br />
sudo apt-get install build-essential cmake unzip pkg-config<br/>
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev<br/>
sudo apt-get install libxvidcore-dev libx264-dev  <br/>
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev<br/>
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev<br/>
sudo apt-get install python3-dev python3-numpy python3-pip<br/>
sudo apt-get install curl wget libssl-dev ca-certificates git libboost-regex-dev<br/>
sudo apt-get install libgtk2.0-dev pkg-config unzip automake libtool autoconf<br/>
sudo apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libgtk2.0-dev<br/>
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base libusb-1.0-0-dev<br/>
sudo apt-get install ffmpeg libjpeg-dev libtiff-dev  git  libtbb2 libtbb-dev<br/>
sudo apt-get install cython cython3 libv4l-dev<br/>
<br/>
**2. pip/python**<br/>
wget https://bootstrap.pypa.io/get-pip.py<br/>
sudo python3 get-pip.py<br/>
sudo -H  pip  install numpy<br/>
sudo -H  pip3 install Cython<br/>
<br/>
**3. Extra nice to have**
sudo apt-get install codeblocks codeblocks-contrib<br/>
sudo apt-get install spyder3<br/>
<br/>
**4. Swapfile Armbian** ( if you want to compile faster, with make -j4)<br/>
 https://linuxize.com/post/how-to-add-swap-space-on-debian-9/<br/>
 <br/>
sudo swapon --show<br/>
sudo fallocate -l 2G /swapfile<br/>
sudo dd if=/dev/zero of=/swapfile bs=1024 count=2048576<br/>
sudo chmod 600 /swapfile<br/>
sudo mkswap /swapfile<br/>
sudo swapon /swapfile<br/>

 *If you whant to make it permanent ..*<br/>
sudo nano /etc/fstab<br/>

 add<br/>
/swapfile swap swap defaults 0 0<br/>
<br/>
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev<br/>
sudo apt-get install libxvidcore-dev libx264-dev  <br/>
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev<br/>
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev<br/>
 **1. apt-get**
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install libxvidcore-dev libx264-dev  
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev
sudo apt-get install python3-dev python3-numpy python3-pip
sudo apt-get install curl wget libssl-dev ca-certificates git libboost-regex-dev
sudo apt-get install libgtk2.0-dev pkg-config unzip automake libtool autoconf
sudo apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libgtk2.0-dev
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base libusb-1.0-0-dev
sudo apt-get install ffmpeg libjpeg-dev libtiff-dev  git  libtbb2 libtbb-dev
sudo apt-get install cython cython3 libv4l-dev

**2. pip/python**
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
sudo -H  pip  install numpy
sudo -H  pip3 install Cython

**3. Extra nice to have**
sudo apt-get install codeblocks codeblocks-contrib
sudo apt-get install spyder3 **1. apt-get**
sudo apt-get update && sudo apt-get upgrade<br />
sudo apt-get install build-essential cmake unzip pkg-config<br/>
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev<br/>
sudo apt-get install libxvidcore-dev libx264-dev  <br/>
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev<br/>
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev<br/>

**4. Swapfile Armbian** ( if you want to compile faster, with make -j4)
 https://linuxize.com/post/how-to-add-swap-space-on-debian-9/
sudo swapon --show
sudo fallocate -l 2G /swapfile
sudo dd if=/dev/zero of=/swapfile bs=1024 count=2048576
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

 *If you whant to make it permanent ..*
sudo nano /etc/fstab

 add
/swapfile swap swap defaults 0 0

**5. OpenCV, select your prefered version**
cd ~
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.0.1.zip
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.1.zip
unzip opencv_contrib.zip
unzip opencv.zip
mv opencv-4.0.1 opencv
mv opencv_contrib-4.0.1 opencv_contrib
cd opencv
mkdir build
cd build

*Todo add more flags of your choice....*
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D BUILD_EXAMPLES=ON -D ENABLE_PRECOMPILED_HEADERS=OFF -DWITH_INF_ENGINE=ON -DENABLE_CXX11=ON  ..
make -j4
sudo make install
 *Note the installation directory of opencv*

**6. Coral**
 https://coral.withgoogle.com/docs/accelerator/get-started/

mkdir coral
cd coral
wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz --trust-server-names
tar xzf edgetpu_api.tar.gz
cd edgetpu_api/
bash ./install.sh

*Minor simple stupid fix for Coral*
cd /usr/local/lib/python3.6/dist-packages/edgetpu/swig/
sudo cp _edgetpu_cpp_wrapper.cpython-35m-aarch64-linux-gnu.so _edgetpu_cpp_wrapper.so

**7. NCS 2**
https://software.intel.com/en-us/articles/ARM64-sbc-and-NCS2
https://github.com/skhameneh/OpenVINO-ARM64

cd ~
mkdir ncs2
cd ncs2
git clone https://github.com/opencv/dldt.git
cd dldt/inference-engine/
git submodule init
git submodule update --recursive

1. apt-get
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install libxvidcore-dev libx264-dev  
sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev
sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev
sudo apt-get install python3-dev python3-numpy python3-pip
sudo apt-get install curl wget libssl-dev ca-certificates git libboost-regex-dev
sudo apt-get install libgtk2.0-dev pkg-config unzip automake libtool autoconf
sudo apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libgtk2.0-dev
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base libusb-1.0-0-dev
sudo apt-get install ffmpeg libjpeg-dev libtiff-dev  git  libtbb2 libtbb-dev
sudo apt-get install cython cython3 libv4l-dev

2. pip/python
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
sudo -H  pip  install numpy
sudo -H  pip3 install Cython
3. Extra nice to have
sudo apt-get install codeblocks codeblocks-contrib
sudo apt-get install spyder3

4. Swapfile Armbian ( if you want to compile faster, with make -j6)
https://linuxize.com/post/how-to-add-swap-space-on-debian-9/
sudo swapon --show
sudo fallocate -l 2G /swapfile
sudo dd if=/dev/zero of=/swapfile bs=1024 count=2048576
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

If you want to make it permanent ..
sudo nano /etc/fstab

 add
/swapfile swap swap defaults 0 0

5. OpenCV, select your prefered version
cd ~
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.0.1.zip
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.1.zip
unzip opencv_contrib.zip
unzip opencv.zip
mv opencv-4.0.1 opencv
mv opencv_contrib-4.0.1 opencv_contrib
cd opencv
mkdir build
cd build

Todo add more flags of your choice....
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D BUILD_EXAMPLES=ON -D ENABLE_PRECOMPILED_HEADERS=OFF -DWITH_INF_ENGINE=ON -DENABLE_CXX11=ON  ..
make -j4
sudo make install
Note the installation directory of opencv

6. Coral
https://coral.withgoogle.com/docs/accelerator/get-started/

mkdir coral
cd coral
wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz --trust-server-names
tar xzf edgetpu_api.tar.gz
cd edgetpu_api/
bash ./install.sh

# Minor simple stupid fix for Coral
cd /usr/local/lib/python3.6/dist-packages/edgetpu/swig/
sudo cp _edgetpu_cpp_wrapper.cpython-35m-aarch64-linux-gnu.so _edgetpu_cpp_wrapper.so

# 7. NCS 2
# https://software.intel.com/en-us/articles/ARM64-sbc-and-NCS2
# https://github.com/skhameneh/OpenVINO-ARM64

cd ~
mkdir ncs2
cd ncs2
git clone https://github.com/opencv/dldt.git
cd dldt/inference-engine/
git submodule init
git submodule update --recursive

# 7.1 Prepare dldt for aarch64 or architecture of your choice
( Check your Machine Hardware Architecture with : uname --m  in my case aarch64 )

# 7.2 Copy more samples from
l_openvino_toolkit_raspbi_p_2019.1.094.tgz

to
~/ncs2/dldt/inference-engine/samples/


Ex, with codeblocks Ctrl+Shift+F  ( find in files )
find  "!defined(_M_ARM)" then add  !defined(__aarch64__)

example : #if !defined(__arm__) && !defined(_M_ARM) && !defined(__aarch64__)

# 7.3 probably not needed ( but why not ;-)
find "armv7l" and add elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")

example
if(CMAKE_SYSTEM_PROCESSOR STREQUAL "armv7l")
    set (ARCH_FOLDER armv7l)
elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")
    set (ARCH_FOLDER aarch64)

# 7.4 probably not needed ( but why not ;-)
Find and update "CMAKE_C_COMPILER"
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR aarch64)
set(CMAKE_C_COMPILER gcc-7)
set(CMAKE_CXX_COMPILER g++-7)


# 7.5 Build inference-engine for C++ & python

# from step 5, depends on your version of OpenCV
export OpenCV_DIR=/usr/include/opencv2


# Todo add more flags of your choice...
# verify -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so  and -DPYTHON_INCLUDE_DIR=/usr/include/python3.6  ( replace with your config )

mkdir build
cd build
cmake -DENABLE_PYTHON=ON -DPYTHON_EXECUTABLE=`which python3.6` -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so -DPYTHON_INCLUDE_DIR=/usr/include/python3.6 -DCMAKE_BUILD_TYPE=Release -DENABLE_MKL_DNN=OFF -DENABLE_CLDNN=OFF -DENABLE_GNA=OFF -DENABLE_SSE42=OFF -DTHREADING=SEQ ..
make -j4

# 7.5 create tools folder
/home/gnu/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/inference_engine/tools

copy from your x86 openvino tools folder to tools  
tools/accuracy_checker
tools/benchmark
tools/calibration
tools/utils
tools/network.py

# 7.6 Simple stupid python "installation"
cd /usr/local/lib/python3.6/dist-packages
sudo mkdir  openvino
cd openvino
sudo cp -r /home/gnu/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/* .

# 8 Needed ? ( seems to work without it )
# from l_openvino_toolkit_raspbi_p_2019.1.094.tgz

cp 97-myriad-usbboot.rules_.txt /etc/udev/rules.d/97-myriad-usbboot.rules
udevadm control --reload-rules
udevadm trigger
ldconfig


Ready !

Test a sample  ( use sudo python3 if it doesn't start )

