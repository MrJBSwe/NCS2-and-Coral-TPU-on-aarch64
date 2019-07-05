**How to install NCS2 Myriad X and Google Coral TPU on aarch64**

This is tested with :

 - Nvidia Jetson Nano ( Ubuntu 18.04 )
 - NanoPi M4 & NanoPi Neo4 ( Armbian 18.04 )
 
 Coral just needs a minor fix, step 6<br />
 OpenCV step 5, is optional if you already have it installed as for Nvidia Jetson Nano.<br />
 Step 7-8 is aimed at NCS2, and builds all C++ dldt inference-engine libraries and ie_api.so for python<br />

 **1. apt-get**<br/>
 <br/>
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
**3. Extra nice to have**<br/>
<br/>
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

 *add*<br/>
/swapfile swap swap defaults 0 0<br/>
<br/>
**5. OpenCV, select your prefered version**<br/>
This step is optional ( intended primary for a clean Armbian )<br/>

cd ~<br/>
wget -O opencv_contrib.zip<br/>
https://github.com/opencv/opencv_contrib/archive/4.0.1.zip<br/>
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.1.zip<br/>
unzip opencv_contrib.zip<br/>
unzip opencv.zip<br/>
mv opencv-4.0.1 opencv<br/>
mv opencv_contrib-4.0.1 opencv_contrib<br/>
cd opencv<br/>
mkdir build<br/>
cd build<br/>

*Todo add more flags of your choice....*<br/>
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D BUILD_EXAMPLES=ON -D ENABLE_PRECOMPILED_HEADERS=OFF -DWITH_INF_ENGINE=ON -DENABLE_CXX11=ON  ..<br/>
make -j4<br/>
sudo make install<br/>
 *Note the installation directory of opencv*<br/>
<br/>
**6. Coral**<br/>
 https://coral.withgoogle.com/docs/accelerator/get-started/<br/>
<br/>
mkdir coral<br/>
cd coral<br/>
wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O<br/>
edgetpu_api.tar.gz --trust-server-names<br/>
tar xzf edgetpu_api.tar.gz<br/>
cd edgetpu_api<br/>
bash ./install.sh<br/>

*Minor simple stupid fix for Coral*<br/>
cd /usr/local/lib/python3.6/dist-packages/edgetpu/swig/<br/>
sudo cp _edgetpu_cpp_wrapper.cpython-35m-aarch64-linux-gnu.so edgetpu_cpp_wrapper.so<br/>
<br/>
**7. NCS 2**<br/>
https://software.intel.com/en-us/articles/ARM64-sbc-and-NCS2<br/>
https://github.com/skhameneh/OpenVINO-ARM64<br/>

cd ~<br/>
mkdir ncs2<br/>
cd ncs2<br/>
git clone https://github.com/opencv/dldt.git<br/>
cd dldt/inference-engine/<br/>
git submodule init<br/>
git submodule update --recursive<br/>
<br/>
**7.1 Prepare dldt for aarch64 or architecture of your choice**<br/>
<br/>
 *Check your Machine Hardware Architecture with : **uname --m**  in my case aarch64*  <br/>
 - Add more samples than comes with dldt
 - Fix #define in samples !defined(__aarch64__)
 - Add aarch64 build folder ( optional )
 - Select compiler ( optional )
 - Select proper python include & library
 - patch output folder with tool from x86 installation
 - install python files
 
<br/>
**7.1.1 Copy more samples from**<br/>
Add more samples than comes with dldt<br/>
<br/>
l_openvino_toolkit_raspbi_p_2019.1.094.tgz<br/>
<br/>
to<br/>
~/ncs2/dldt/inference-engine/samples/<br/>
<br/>
*Ex, with codeblocks Ctrl+Shift+F  ( find in files )*<br/>
find  "!defined(_M_ARM)" then add  !defined(__aarch64__)<br/>
<br/>
example : #if !defined(__arm__) && !defined(_M_ARM) && !defined(__aarch64__)<br/>
<br/>
**7.1.2 probably not needed** ( but why not ;-)<br/>
Add aarch64 build folder<br/>
<br/>
find "armv7l" and add elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")<br/>
<br/>
*example*<br/>
if(CMAKE_SYSTEM_PROCESSOR STREQUAL "armv7l")<br/>
    set (ARCH_FOLDER armv7l)<br/>
elseif(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")<br/>
    set (ARCH_FOLDER aarch64)<br/>
<br/>

**7.1.3 probably not needed** ( but why not ;-)<br/>
Select compiler<br/>
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
export OpenCV_DIR=/usr/include/opencv2  ( Nvidia Jetson nano ) <br/>
or<br/>
export OpenCV_DIR=/usr/local/include/opencv4 ( Install from source )<br/>
 <br/>
<br/>
*verify -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so*<br/>
 *verify DPYTHON_INCLUDE_DIR=/usr/include/python3.6*<br/>   
<br/>

cd ~/ncs2/dldt/inference-engine<br/>
mkdir build<br/>
cd build<br/>
*Todo add more flags of your choice...*<br/>
cmake -DENABLE_PYTHON=ON -DPYTHON_EXECUTABLE=`which python3.6` -DPYTHON_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.6m.so -DPYTHON_INCLUDE_DIR=/usr/include/python3.6 -DCMAKE_BUILD_TYPE=Release -DENABLE_MKL_DNN=OFF -DENABLE_CLDNN=OFF -DENABLE_GNA=OFF -DENABLE_SSE42=OFF -DTHREADING=SEQ ..<br/>
make -j4<br/>
<br/>
**7.3 create tools folder**<br/>
patch output folder with tool from x86 installation<br/>
<br/>
~/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/inference_engine/**tools**<br/>
<br/>
*copy from your x86 openvino tools folder to tools*  <br/>
tools/accuracy_checker<br/>
tools/benchmark<br/>
tools/calibration<br/>
tools/utils<br/>
tools/network.py<br/>
<br/>
**7.4 Simple stupid python installation**<br/>
install python files<br/>
<br/>
cd /usr/local/lib/python3.6/dist-packages<br/>
sudo mkdir  openvino<br/>
cd openvino<br/>
sudo cp -r ~/ncs2/dldt/inference-engine/bin/aarch64/Release/lib/python_api/python3.6/openvino/* .<br/>
<br/>
 **8 Needed myriad-rules ?** ( seems to work without it )<br/>
*from l_openvino_toolkit_raspbi_p_2019.1.094.tgz*<br/>

cp 97-myriad-usbboot.rules_.txt /etc/udev/rules.d/97-myriad-usbboot.rules<br/>
udevadm control --reload-rules<br/>
udevadm trigger<br/>
ldconfig<br/>
<br/>

**Ready !**<br/>
<br/>
Test a sample  ( if it doesn't start ..try use sudo python3  )<br/>


