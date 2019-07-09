**How to install NCS2 Myriad X and Google Coral TPU on aarch64 (ARM64)**

This is tested with :

 - Nvidia Jetson Nano ( Ubuntu 18.04 )
 - NanoPi M4 & NanoPi Neo4 ( Armbian 18.04 )
 
 Coral just needs a minor fix, step 6<br />
 OpenCV step 5, is optional if you already have it installed (Nvidia Jetson Nano)<br />
 Step 7-8 is aimed at NCS2, and builds all C++ dldt inference-engine libraries and ie_api.so for python<br />

 **1. apt-get**<br/>
 <br/>
 ```bash
$sudo apt-get update && sudo apt-get upgrade
$sudo apt-get install build-essential cmake unzip pkg-config
$sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
$sudo apt-get install libxvidcore-dev libx264-dev  
$sudo apt-get install libgtk-3-dev libopenblas-dev libpng-dev
$sudo apt-get install libatlas-base-dev gfortran libdc1394-22-dev
$sudo apt-get install python3-dev python3-numpy python3-pip
$sudo apt-get install curl wget libssl-dev ca-certificates git libboost-regex-dev
$sudo apt-get install libgtk2.0-dev pkg-config unzip automake libtool autoconf
$sudo apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libgtk2.0-dev
$sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base libusb-1.0-0-dev
$sudo apt-get install ffmpeg libjpeg-dev libtiff-dev  git  libtbb2 libtbb-dev
$sudo apt-get install cython cython3 libv4l-dev
```
<br/>

**2. pip/python**<br/>
```bash
$wget https://bootstrap.pypa.io/get-pip.py
$sudo python3 get-pip.py
$sudo -H  pip  install numpy
$sudo -H  pip3 install Cython
```
<br/>

**3. Extra nice to have**<br/>
<br/>
 ```bash
$sudo apt-get install codeblocks codeblocks-contrib
$sudo apt-get install spyder3
```
<br/>

**4. Swapfile Armbian** if you want to compile faster, with make -j4 <br/>
<br/>
 https://linuxize.com/post/how-to-add-swap-space-on-debian-9/<br/>
 <br/>
 ```bash
$sudo swapon --show
$sudo fallocate -l 2G /swapfile
$sudo dd if=/dev/zero of=/swapfile bs=1024 count=2048576
$sudo chmod 600 /swapfile
$sudo mkswap /swapfile
$sudo swapon /swapfile
```
<br/>

```bash
$sudo nano /etc/fstab
/swapfile swap swap defaults 0 0 # Add this to make it permanent
```
<br/>

**5. OpenCV, select your prefered version**<br/>
This step is optional ( intended primary for a clean Armbian )<br/>
<br/>
```bash
$cd ~
$wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.0.1.zip
$wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.1.zip
$unzip opencv_contrib.zip 
$unzip opencv.zip
$mv opencv-4.0.1 opencv
$mv opencv_contrib-4.0.1 opencv_contrib
$cd opencv
$mkdir build
$cd build
```
<br/>

*Todo add more flags of your choice....and note opencv directory*<br/>
<br/>
```bash
$cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D BUILD_EXAMPLES=ON -D ENABLE_PRECOMPILED_HEADERS=OFF -DWITH_INF_ENGINE=ON -DENABLE_CXX11=ON  ..
$make -j4
$sudo make install
```
<br/>
 
**6. Coral**<br/>
 https://coral.withgoogle.com/docs/accelerator/get-started/<br/>
<br/>
```bash
$cd ~ 
$mkdir coral 
$cd coral 
$wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz --trust-server-names 
$tar xzf edgetpu_api.tar.gz 
$cd edgetpu_api 
$bash ./install.sh 
```
<br/>

*Minor simple stupid fix for Coral*<br/>
```bash
$cd /usr/local/lib/python3.6/dist-packages/edgetpu/swig/
$sudo cp _edgetpu_cpp_wrapper.cpython-35m-aarch64-linux-gnu.so edgetpu_cpp_wrapper.so
```
<br/>

**7. NCS 2**<br/>
https://software.intel.com/en-us/articles/ARM64-sbc-and-NCS2<br/>
https://github.com/skhameneh/OpenVINO-ARM64<br/>
```bash
$cd ~
$mkdir ncs2
$cd ncs2
$git clone https://github.com/opencv/dldt.git
$cd dldt/inference-engine/
$git submodule init
$git submodule update --recursive
```
<br/>

**7.1 Prepare dldt for aarch64 or architecture of your choice**<br/>
<br/>
 *Check your machine hardware architecture with : **uname --m**  in my case aarch64*  <br/>
 - Add more samples than comes with dldt
 - Fix #define in samples !defined(__aarch64__)
 - Add aarch64 build folder ( optional )
 - Select compiler ( optional )
 - Select proper python include & library
 - patch output folder with tool from x86 installation
 - install python files
<br/>

**7.1.1 Add more samples than comes with dldt**<br/>
<br/>
from<br/>
l_openvino_toolkit_raspbi_p_2019.1.094.tgz<br/>
<br/>
to<br/>
```bash
$~/ncs2/dldt/inference-engine/samples/
```
<br/>

**7.1.2 Fix defines in samples**<br/>
*Ex, with codeblocks Ctrl+Shift+F  ( find in files )*<br/>
find  "!defined(_M_ARM)" then add **&& !defined(__aarch64__)**<br/>
<br/>
example : #if !defined(__arm__) && !defined(_M_ARM) && !defined(__aarch64__)<br/>
<br/>

**7.1.3 Add aarch64 build folder** ( optional )<br/>
<br/>
find "armv7l" and add elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")<br/>
<br/>
*example*<br/>
if(CMAKE_SYSTEM_PROCESSOR STREQUAL "armv7l")<br/>
    set (ARCH_FOLDER armv7l)<br/>
elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")<br/>
    set (ARCH_FOLDER aarch64)<br/>
<br/>

**7.1.4 Select compiler** ( optional )<br/>
<br/>
Find and update "CMAKE_C_COMPILER"<br/>
set(CMAKE_SYSTEM_NAME Linux)<br/>
set(CMAKE_SYSTEM_PROCESSOR aarch64)<br/>
set(CMAKE_C_COMPILER gcc-7)<br/>
set(CMAKE_CXX_COMPILER g++-7)<br/>
<br/>

**7.2 Build inference-engine for C++ & python**<br/>
<br/>
*from step 5, depends on your version of OpenCV*<br/>

```bash
$export OpenCV_DIR=/usr/include/opencv2       # Nvidia Jetson nano 
```

or<br/>
```bash
$export OpenCV_DIR=/usr/local/include/opencv4 # Install from source  
```
 <br/>
 
<br/>
*verify -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so*<br/>
 *verify DPYTHON_INCLUDE_DIR=/usr/include/python3.6*<br/>   
<br/>
```bash
$cd ~/ncs2/dldt/inference-engine<br/>
$mkdir build<br/>
$cd build<br/>
$ #Todo add more flags of your choice... 
$cmake -DENABLE_PYTHON=ON -DPYTHON_EXECUTABLE=\`which python3.6\` -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so -DPYTHON_INCLUDE_DIR=/usr/include/python3.6 -DCMAKE_BUILD_TYPE=Release -DENABLE_MKL_DNN=OFF -DENABLE_CLDNN=OFF -DENABLE_GNA=OFF -DENABLE_SSE42=OFF -DTHREADING=SEQ ..<br/>
$make -j4<br/>
```
<br/>

**7.3 create tools folder**<br/>
patch output folder with tool from x86 installation<br/>
<br/>
```bash
~/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/inference_engine/tools
```

<br/>
*copy from your x86 openvino tools folder to tools* 
```bash
tools/accuracy_checker
tools/benchmark
tools/calibration
tools/utils
tools/network.py
```
<br/>

**7.4 Simple stupid python installation**<br/>
<br/>
```bash
$cd /usr/local/lib/python3.6/dist-packages 
$sudo mkdir  openvino 
$cd openvino 
$sudo cp -r ~/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/* . 
```
<br/>

 **8 Needed myriad-rules ?** ( seems to work without it )<br/>
*from l_openvino_toolkit_raspbi_p_2019.1.094.tgz*<br/>
```bash
cp 97-myriad-usbboot.rules_.txt /etc/udev/rules.d/97-myriad-usbboot.rules
udevadm control --reload-rules
udevadm trigger
ldconfig 
```
<br/>

**Ready !**<br/>
<br/>
Test a sample  ( if it doesn't start ..try use sudo python3  )<br/>


